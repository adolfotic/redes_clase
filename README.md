## Diagrama: Router-on-a-Stick para Enrutamiento de VLANs

```mermaid
graph TD
    SW(Switch L2)
    R(Router)
    INT[Internet]

    subgraph LAN [Red Local]
        subgraph VLAN_10 [VLAN 10: Dept A (192.168.10.0/24)]
            PCA[PC A] --- P10[Port F1 Access]
        end

        subgraph VLAN_20 [VLAN 20: Dept B (192.168.20.0/24)]
            PCB[PC B] --- P20[Port F2 Access]
        end
        
        subgraph VLAN_30 [VLAN 30: Servidores (192.168.30.0/24)]
            SERVER[Servidor] --- P30[Port F3 Access]
        end

        P10 --- SW
        P20 --- SW
        P30 --- SW
    end

    SW --- |"F4 Trunk (802.1Q)"| R

    subgraph Subinterfaces [Subinterfaces Router (G0/1)]
        R_10[GW: 192.168.10.1 / VLAN 10] --- R
        R_20[GW: 192.168.20.1 / VLAN 20] --- R
        R_30[GW: 192.168.30.1 / VLAN 30] --- R
    end

    R --- |"WAN / ISP"| INT
