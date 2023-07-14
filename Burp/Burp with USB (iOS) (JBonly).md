# Burp with USB (iOS) (JBonly)

TO use burp with USB need to have:

- iproxy
- burp
- USB wire with data transfer
- Jailbreaked iOS device with

To install iproxy, you need libusbmuxd-tools installed

1. iOS with ssh enabled
2. connect iOS device with USB
3. enable iproxy on ssh with port 2222

`iproxy 2222 22`

1. make a remote port forwarding to the <listen port> of burp (eg.8080) 

`ssh -R 8080:localhost:8080 root@localhost -p 2222`

1. Go to 127.0.0.1:<listen port> to get cert
2. set proxy ip to 127.0.0.1, port to <listen port>