# Provisionamento e Conectividade de Máquinas Virtuais (Azure)

## Visão Geral
Documentação da infraestrutura de duas Máquinas Virtuais (VMs) alocadas no Resource Group `5-semestre`, operando dentro da mesma Virtual Network (VNet) para validação de conectividade interna.

## Topologia de Rede e Ambiente
* **Provedor / Região:** Microsoft Azure / Mexico Central (mexicocentral)
* **Resource Group:** `5-semestre`
* **Virtual Network (VNet):** `vnet-mexicocentral-1`
* **Sub-redes:** `snet-mexicocentral-1`

## Especificações das Máquinas Virtuais

| Recurso | VM 01 (`nuem1808`) | VM 02 (`Teste`) |
| :--- | :--- | :--- |
| **Sistema Operacional** | Windows 11 Pro (25H2) | Windows 11 Pro (25H2) |
| **Tamanho (SKU)** | Standard_B2as_v2 | Standard_B2as_v2 |
| **Usuário Admin** | MatheusHenrique | MatheusHenriqueDevz |
| **Zona de Disponibilidade** | Não definida | Zona 1 |
| **Interface de Rede (NIC)** | `nuem1808529` | `teste775` |
| **IP Privado** | 172.16.0.4 | 172.16.1.4 |

## Configuração de Segurança e Conectividade (ICMP/Ping)

A comunicação via protocolo ICMP (Ping) entre as máquinas exigiu a liberação de regras em duas camadas distintas para contornar os bloqueios de segurança padrão:

1. **Camada de Nuvem (Network Security Group - NSG):**
   * Validação de que as regras Inbound do NSG do Azure associado às sub-redes permitiam o tráfego interno na VNet.

2. **Camada de Sistema Operacional (Firewall do Windows):**
   * O Windows 11 bloqueia requisições de Ping (Echo Request) por padrão. Foi necessário aplicar a seguinte regra via PowerShell em ambas as instâncias para aceitar a entrada dos pacotes:
     ```powershell
     New-NetFirewallRule -DisplayName "Allow ICMPv4-In" -Protocol ICMPv4 -IcmpType 8 -Direction Inbound -Action Allow
     ```
## Imagens

<img width="1334" height="123" alt="image" src="https://github.com/user-attachments/assets/8f33e555-b6a4-4825-bfd3-868549be1170" />
<img width="1375" height="774" alt="image" src="https://github.com/user-attachments/assets/7325c2ac-84a3-42a6-ad65-65bb73ac1efe" />

