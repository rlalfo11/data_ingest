미디어플랫폼 성장전략 UNIT _ 07628 _ 김일해 수석

1) 수정한 spooldir.conf 파일
 # Naming the components on the current agent
 agent1.sources = Netcat
 agent1.channels = MemChannel
 agent1.sinks = LoggerSink

 # Describing/Configuring the source
 agent1.sources.Netcat.type = netcat
 agent1.sources.Netcat.bind = localhost
 agent1.sources.Netcat.port = 44444

 # Describing/Configuring the sink
 agent1.sinks.LoggerSink.type = logger

 # Describing/Configuring the channel
 agent1.channels.MemChannel.type = memory
 agent1.channels.MemChannel.capacity = 1000
 agent1.channels.MemChannel.transactionCapacity = 100

 # Bind the source and sink to the channel
 agent1.sources.Netcat.channels = MemChannel
 agent1.sinks.LoggerSink.channel = MemChannel


2) 명령어
flume-ng agent --conf /etc/flume-ng/conf --conf-file ./spooldir.conf --name agent1 -Dflume.root.logger=INFO,console

3) 명령 수행 결과
[training@localhost Documents]$ telnet localhost 44444
Trying 127.0.0.1...
telnet: connect to address 127.0.0.1: Connection refused
Trying ::1...
telnet: connect to address ::1: Network is unreachable
[training@localhost Documents]$ telnet localhost 44444
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
