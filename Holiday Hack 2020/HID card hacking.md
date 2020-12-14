## Reader mechanism

- Reader takes in a unique (8bit) **Facility code**  and an unique **card ID** (16 bit)
- Reader sends the facility code using **Wiegand**  protocol to the backend 
- Backend checks if the card is allowed to carry on an action

## Proxmark3

- RFID research tool
- Interrogate and emulate tags(recieve and transmit the data as if it was a card)

### Proxcard Read and Simulate (clonig attacks)
- Capture:
	- `lf hid read`
- Simulate
	- `lf hid sim -r <raw datta>`

### Clone HID ProxCard
- Search for nearby card:
	- `lf search`
- clone the card
	- `lf hid clone <raw data>`


## Cards Ids

- 2006e22f0d
- 2006e22f31
- 2006e22f13