# COSMOS CFDP Engine (cosmos v4.1.1)

[![AUR](https://img.shields.io/aur/license/yaourt.svg)](https://github.com/edipovisiona/cfdp-engine/blob/master/LICENSE)

## What does it do

- Class 1, 2 file transfer
- Downlink and Uplink
- Immediate mode
- Tested with Ubuntu 14.10, Windows 10 x64

## Getting started

Be sure that 'pathtoyourcosmos' is your custom cosmos project folder name, such as 'demo'.

1) Copy config/targets/ to your 'pathtoyourcosmos/config/targets/', which will include targets CFDP and PDU

2) Copy lib/ contents to your 'pathtoyourcosmos/lib/'. That will include cfdp and utils_visiona to your custom cosmos project.

3) Declare both targets at 'pathtoyourcosmos/config/system.txt'

```
DECLARE TARGET CFDP
DECLARE TARGET CFDP_TEST
DECLARE TARGET PDU
```

4) All following configurations happens at your cmd_tlm_server definition, which is 'pathtoyourcosmos/config/tools/cmd_tlm_server/cmd_tlm_server.txt'. Main interface is the interface configured to directly send data to OBDH:

4.1) Add background task

```
BACKGROUND_TASK cfdp_engine_task.rb
```

4.2) Add CFDP interface + target (This will use definitions provided at CFDP folder)

```
INTERFACE_TARGET CFDP cmd_tlm_server.txt
```

4.3) Add PDU and CFDP_TEST targets to your main interface

```
INTERFACE MAIN_INT...
TARGET PDU
TARGET CFDP_TEST
```

4.4) Add CFDP and CFDP_TEST protocols (must respect this order) to your main interface

```
INTERFACE MAIN_INT...
  PROTOCOL READ interfaces/cfdp_test_protocol
  PROTOCOL READ interfaces/cfdp_protocol
  PROTOCOL WRITE interfaces/cfdp_protocol  
  PROTOCOL WRITE interfaces/cfdp_test_protocol
```

Done. CFDP Engine should now work, and you will be able to check it's cmd/tlm within Command and Telemetry Server.

## License

GPL3
