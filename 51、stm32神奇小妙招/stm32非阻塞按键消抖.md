- 定时器扫描按键-单按键
定时中断，每隔20ms读取一次本次引脚值和上次引脚值
判断：如果本次是1，上次是0，则表示按键按下且当前处于刚松手的状态
```c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"
#include "oled.h"
void App_PWM_Init(void);
void App_Button_Init(void);
uint8_t key_GetState(void);
void TIM2_IRQHandler(void);
void key_Tick(void);
uint8_t key_GetNum(void);

uint16_t pwm_value = 0;
int8_t pwm_dir = 1;  
uint16_t pwm_step[5]={4,8,13,25,50};
uint8_t cnt=3;
uint8_t key_Num;
int main(void)
{
	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
	App_PWM_Init();
	App_Button_Init();
	
	while(1)
	{
		uint8_t key=key_GetNum();
		if(key == 1)
		{
			cnt++;
			if(cnt>5) cnt=1;
		}
		else if(key == 2)
		{
			cnt--;
			if(cnt==0) cnt=5;
		}
		
		pwm_value+=pwm_dir*pwm_step[cnt-1];
		if(pwm_value>=999)
		{
			pwm_dir=-1;
			pwm_value=999;
		}
		else if (pwm_value <= 0)
        {
            pwm_dir = 1;
            pwm_value = 0;
        }
		TIM_SetCompare1(TIM1,pwm_value);
		Delay(7);
	}
}

void App_PWM_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA,ENABLE);
	GPIO_InitTypeDef GPIO_InitStruct;
	GPIO_InitStruct.GPIO_Pin=GPIO_Pin_8;
	GPIO_InitStruct.GPIO_Mode=GPIO_Mode_AF_PP;
	GPIO_InitStruct.GPIO_Speed=GPIO_Speed_2MHz;
	GPIO_Init(GPIOA,&GPIO_InitStruct);
	
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_TIM1,ENABLE);
	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStruct;
	TIM_TimeBaseInitStruct.TIM_Prescaler=71;
	TIM_TimeBaseInitStruct.TIM_Period=999;
	TIM_TimeBaseInitStruct.TIM_CounterMode=TIM_CounterMode_Up;
	TIM_TimeBaseInitStruct.TIM_RepetitionCounter=0;
	TIM_TimeBaseInit(TIM1,&TIM_TimeBaseInitStruct);
	TIM_Cmd(TIM1,ENABLE);
	
	TIM_ARRPreloadConfig(TIM1,ENABLE);
	
	TIM_OCInitTypeDef TIM_OCInitStruct;
	TIM_OCInitStruct.TIM_OCMode=TIM_OCMode_PWM1;
	TIM_OCInitStruct.TIM_OCPolarity=TIM_OCPolarity_High;
	TIM_OCInitStruct.TIM_OutputState=ENABLE;
	TIM_OCInitStruct.TIM_OCNPolarity=TIM_OCNPolarity_High;
	TIM_OCInitStruct.TIM_OutputNState=DISABLE;
	TIM_OCInitStruct.TIM_Pulse=0;
	TIM_OC1Init(TIM1,&TIM_OCInitStruct);
	TIM_CtrlPWMOutputs(TIM1,ENABLE);
	TIM_CCPreloadControl(TIM1,ENABLE);
}

void App_Button_Init(void)
{
	GPIO_InitTypeDef GPIO_InitStruct;
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB,ENABLE);
	GPIO_InitStruct.GPIO_Pin=GPIO_Pin_14|GPIO_Pin_15;
	GPIO_InitStruct.GPIO_Mode=GPIO_Mode_IPU;
	GPIO_InitStruct.GPIO_Speed=GPIO_Speed_2MHz;
	GPIO_Init(GPIOB,&GPIO_InitStruct);
	
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2,ENABLE);
	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStruct;
	TIM_TimeBaseInitStruct.TIM_Prescaler=71;
	TIM_TimeBaseInitStruct.TIM_Period=999;
	TIM_TimeBaseInitStruct.TIM_CounterMode=TIM_CounterMode_Up;
	TIM_TimeBaseInitStruct.TIM_ClockDivision=0;
	TIM_TimeBaseInit(TIM2,&TIM_TimeBaseInitStruct);
	
	TIM_ITConfig(TIM2,TIM_IT_Update,ENABLE);
	
	NVIC_InitTypeDef NVIC_InitStruct;
	NVIC_InitStruct.NVIC_IRQChannel=TIM2_IRQn;
	NVIC_InitStruct.NVIC_IRQChannelPreemptionPriority=1;
	NVIC_InitStruct.NVIC_IRQChannelSubPriority=0;
	NVIC_InitStruct.NVIC_IRQChannelCmd=ENABLE;
	NVIC_Init(&NVIC_InitStruct);
	
	TIM_Cmd(TIM2,ENABLE);
}

uint8_t key_GetState(void)
{
	if(GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_14) == 0)
	{
		return 1;
	}
	if(GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_15) == 0)
	{
		return 2;
	}
	return 0;
}

void TIM2_IRQHandler(void)
{
	if(TIM_GetITStatus(TIM2, TIM_IT_Update) == SET)
	{
		key_Tick();  // 执行按键消抖状态机
		TIM_ClearITPendingBit(TIM2, TIM_IT_Update);  // 清除中断标志
	}
}

void key_Tick(void)
{
	static uint8_t Count = 0;
	static uint8_t CurrState = 0;
	static uint8_t PrevState = 0;

	Count++;
	if(Count >= 20)
	{
		Count = 0;
		PrevState = CurrState;
		CurrState = key_GetState();

		if(CurrState == 0 && PrevState != 0)
		{
			key_Num = PrevState;
		}
	}
}

uint8_t key_GetNum(void)
{
	uint8_t Temp = 0;
	
	if(key_Num != 0)
	{
		Temp = key_Num;
		key_Num = 0;
		return Temp;
	}
	return 0;
}

```
```c

```
```c

```