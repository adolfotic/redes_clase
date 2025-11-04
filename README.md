```mermaid
graph TD
    subgraph LAN [Red Local]
        subgraph VLAN_10 [VLAN 10: Departamento A]
            PC_A[PC A 192.168.10.10] --- Switch_Port_F1  <-- ¡Revisar esta línea!
        end

        subgraph VLAN_20 [VLAN 20: Departamento B]
            PC_B[PC B 192.168.20.10] --- Switch_Port_F2
        end

        subgraph VLAN_30 [VLAN 30: Servidores]
            SERVER[Servidor 192.168.30.10] --- Switch_Port_F3
        end

        Switch_Port_F1[F1 (Access VLAN 10)] --- Switch(Switch L2)
        Switch_Port_F2[F2 (Access VLAN 20)] --- Switch
        Switch_Port_F3[F3 (Access VLAN 30)] --- Switch

        Switch --- |"**F4 (Trunk)** Etiquetado 802.1Q"| Router(Router)
    end

    Router --- |"**GigabitEthernet0/1**"| INTERNET[Internet]

    subgraph Router_Subinterfaces [Router: Interfaz Física G0/1]
        Router_G0_1_10["G0/1.10 (Encapsulación 802.1Q 10) -> GW: 192.168.10.1"] --- Router
        Router_G0_1_20["G0/1.20 (Encapsulación 802.1Q 20) -> GW: 192.168.20.1"] --- Router
        Router_G0_1_30["G0/1.30 (Encapsulación 802.1Q 30) -> GW: 192.168.30.1"] --- Router
    end
