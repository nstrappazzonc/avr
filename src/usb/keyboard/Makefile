TARGET=atmega32u2keypad
MCU=atmega32u2
CFLAGS=-Os -mmcu=$(MCU) -DF_CPU=16000000UL
CXXFLAGS=$(CFLAGS)
LDFLAGS=-mmcu=$(MCU)

all: $(TARGET).hex

%.o: %.c
	avr-gcc -c $(CFLAGS) $^ -o $@

%.o: %.cpp
	avr-g++ -c $(CXXFLAGS) $^ -o $@

$(TARGET).elf: main.o usb.o
	avr-g++ $(LDFLAGS) $^ -o $(TARGET).elf

$(TARGET).hex: $(TARGET).elf
	avr-objcopy -O ihex -R .eeprom -R .fuse -R .lock -R .signature $^ $@

clean:
	rm -f *.o
	rm -f *.elf
	rm -f *.hex

upload: ## Write firmware to microcontroller.
	avrdude -F -V -c usbtiny -p atmega32u2 -U flash:w:atmega32u2keypad.hex
