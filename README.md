# SINAV222
yazılı
from machine import Pin, ADC, PWM
from machine import Pin, SoftI2C
from time import sleep 
import ssd1306

led = Pin(15, Pin.OUT)
button = Pin(23, Pin.IN)


pot = ADC(Pin(34))
pot.width(ADC.WIDTH_10BIT)
pot.atten(ADC.ATTN_11DB)


led_pwm = PWM(Pin(4),5000)

while True:
  button_state = button.value()
  led.value(button_state)

    pot_value = pot.read()
    led_pwm.duty(pot_value)

    sleep(0.01)

 
    i2c = SoftI2C(scl=Pin(22), sda=Pin(21))

    oled_width = 128
    oled_height = 64
    oled = ssd1306.SSD1306_I2C(oled_width, oled_height, i2c)

    oled.text(str(pot_value), 0, 0)

        
    oled.show()
