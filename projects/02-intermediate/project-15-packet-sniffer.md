# Project 15: Network Packet Sniffer

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a network packet analyzer using gopacket. Learn packet capture, protocol parsing, and network traffic analysis.

**Difficulty:** Intermediate  
**Estimated Time:** 20-30 hours

## Prerequisites

**Required Packages:**
```bash
go get github.com/google/gopacket
sudo apt-get install libpcap-dev  # Linux
brew install libpcap              # macOS
```

## What You'll Learn

- Packet capture with gopacket
- Protocol parsing (Ethernet, IP, TCP, UDP)
- BPF filters
- Traffic analysis
- Protocol detection
- Network forensics

## Implementation Guide

```go
package main

import (
    "fmt"
    "github.com/google/gopacket"
    "github.com/google/gopacket/layers"
    "github.com/google/gopacket/pcap"
    "log"
)

func main() {
    device := "eth0"
    snapshotLen := int32(1600)
    promiscuous := false
    timeout := pcap.BlockForever
    
    handle, err := pcap.OpenLive(device, snapshotLen, promiscuous, timeout)
    if err != nil {
        log.Fatal(err)
    }
    defer handle.Close()
    
    // Set BPF filter
    filter := "tcp and port 80"
    handle.SetBPFFilter(filter)
    
    packetSource := gopacket.NewPacketSource(handle, handle.LinkType())
    
    for packet := range packetSource.Packets() {
        printPacketInfo(packet)
    }
}

func printPacketInfo(packet gopacket.Packet) {
    // Ethernet layer
    ethernetLayer := packet.Layer(layers.LayerTypeEthernet)
    if ethernetLayer != nil {
        eth := ethernetLayer.(*layers.Ethernet)
        fmt.Printf("Src MAC: %s, Dst MAC: %s\n", eth.SrcMAC, eth.DstMAC)
    }
    
    // IP layer
    ipLayer := packet.Layer(layers.LayerTypeIPv4)
    if ipLayer != nil {
        ip := ipLayer.(*layers.IPv4)
        fmt.Printf("Src IP: %s, Dst IP: %s\n", ip.SrcIP, ip.DstIP)
    }
    
    // TCP layer
    tcpLayer := packet.Layer(layers.LayerTypeTCP)
    if tcpLayer != nil {
        tcp := tcpLayer.(*layers.TCP)
        fmt.Printf("Src Port: %d, Dst Port: %d\n", tcp.SrcPort, tcp.DstPort)
        fmt.Printf("Flags: SYN=%v, ACK=%v, FIN=%v\n", tcp.SYN, tcp.ACK, tcp.FIN)
    }
    
    // Application layer
    applicationLayer := packet.ApplicationLayer()
    if applicationLayer != nil {
        fmt.Printf("Payload: %s\n", applicationLayer.Payload())
    }
}
```

## Project Structure

```
packet-sniffer/
├── main.go
├── capture/
│   ├── sniffer.go
│   └── filter.go
├── protocol/
│   ├── ethernet.go
│   ├── ip.go
│   ├── tcp.go
│   └── http.go
├── analysis/
│   └── stats.go
└── README.md
```

## Next Steps

- Add HTTP request/response parsing
- Implement PCAP file writing
- Create TUI interface
- Move to [Project 16: System Call Tracer](project-16-syscall-tracer.md)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
