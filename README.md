```mermaid
graph TD
    subgraph LAN [Red Local]
        subgraph VLAN_10 [VLAN 10: Dept A]
            PCA[PC A 192.168.10.10] --- F1_10(F1 Access VLAN 10)
        end

        subgraph VLAN_20 [VLAN 20: Dept B]
            PCB[PC B 192.168.20.10] --- F2_20(F2 Access VLAN 20)
        end

        subgraph VLAN_30 [VLAN 30: Servidores]
            SERVER[Servidor 192.168.30.10] --- F3_30(F3 Access VLAN 30)
        end
        
        % Conexiones internas al Switch L2
        F1_10 --- SW(Switch L2)
        F2_20 --- SW
        F3_30 --- SW

        SW --- |"F4 Trunk (802.1Q)"| Router(Router)
    end

    Router --- |"GigabitEthernet0/1"| INTERNET[Internet]

    subgraph Router_Subinterfaces [Router Subinterfaces]
        G0_1_10["G0/1.10 (GW: 192.168.10.1)"] --- Router
        G0_1_20["G0/1.20 (GW: 192.168.20.1)"] --- Router
        G0_1_30["G0/1.30 (GW: 192.168.30.1)"] --- Router
    end
