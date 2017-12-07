CFDP Engine works for both Linux/Windows systems (tested with Ubuntu 16.10 and Windows 10 x64).

To include CFDP Engine in your COSMOS' project, follow these steps (be sure that 'pathtoyourcosmos' is your custom cosmos' project name, such as 'demo'):

1) copy CFDP and PDU folders to 'pathtoyourcosmos/config/targets/'

2) copy cfdp source code folder to 'pathtoyourcosmos/lib/'

3) copy utils_visiona source code folder to 'pathtoyourcosmos/lib/'

4) declare both targets at pathtoyourcosmos/config/system.txt
  - DECLARE TARGET CFDP
  - DECLARE TARGET PDU

5) add background task at 'pathtoyourcosmos/config/tools/cmd_tlm_server/cmd_tlm_server.txt'
  - BACKGROUND_TASK cfdp_engine_task.rb

6) add cfdp protocol to your interface. You must have a custom interface (or change cosmos' source code), for e.g.:
  - class VisionaUdpInterface < UdpInterface
  - add_protocol(CFDPProtocol, [], :READ_WRITE)

7) add PDU and CFDP targets to your custom interface
  - TARGET PDU
  - TARGET CFDP

Done. 
CFDP Engine should now work, and you will be able to check it's cmd/tlm within Command and Telemetry Server.
