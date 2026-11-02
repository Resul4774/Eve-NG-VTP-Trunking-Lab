# VTP ve 802.1Q Trunking Lab (Eve-NG)

Bu proje, Cisco switch'lerde VLAN Trunking Protocol (VTP) ve 802.1Q Trunk yapılandırmalarının Eve-NG ortamında uygulanmasını gösterir. 

## 🎯 Amaç
- VTP Server, Client ve Transparent modlarını yapılandırmak.
- Trunk port ve Native VLAN (VLAN 99) ayarlarını yapmak.
- VLAN bilgilerinin Server'dan Client'a otomatik senkronize olduğunu doğrulamak.

## 🏗️ Topoloji
[SW1-Server] --(Trunk)-- [SW2-Transparent] --(Trunk)-- [SW3-Client]

- **VTP Domain:** CORP
- **VTP Password:** cisco123
- **VLANs:** 10 (SATIS), 20 (MUHASEBE), 30 (IT), 99 (MANAGEMENT)

## ⚙️ Temel Yapılandırma

**1. VTP Ayarları (Tüm switch'lerde):**
```cisco
vtp domain CORP
vtp password cisco123
vtp version 2
vtp mode {server | client | transparent}

2. Trunk Port Ayarları (Bağlantı yapılan portlarda):
interface Ethernet0/0
 switchport mode trunk
 switchport trunk native vlan 99
 switchport nonegotiate

3. VLAN Oluşturma (Sadece SW1-Server'da):
vlan 10
 name SATIS
vlan 99
 name MANAGEMENT

✅ Doğrulama
Aşağıdaki komutlarla yapılandırmanın başarılı olduğu teyit edilir:
show vtp status → Domain, mod ve Revision Number'ın eşleştiğini kontrol et.
show vlan brief → Client switch'te VLAN'ların otomatik oluştuğunu gör.
show interfaces trunk → Portların trunk modunda ve Native VLAN'ın 99 olduğunu doğrula.
