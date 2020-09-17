# CCNA2020_DynamicRouting
動態路由，由軟體輸入 route entry，倘若整個網域內有主機 ip 位址異動，網管人員不必手動更新，動態路由規則功能會幫助我們自動更新。


# 架構圖範例


                                 Internet (WAN)
                                 
                                       |
                                       |
                                       |
                                       
                                     (LAN)
                                     
                                       |
                                       |
                                       |
                                     
                                    Router 1
                                    
                                    NIC1: NAT (public ip)
                                    NIC2: 192.168.0.254 (private ip)
                                    
                                      /                    \
                                     /                      \
                                    /                        \
                                    
                               (Protecte LAN)                (Protecte LAN)
                        
                             Router 2                          Router 3
                       NIC1:192.168.0.2/24    --- SW 3 ---   NIC1:192.168.0.3/24
                       NIC2:192.168.5.254/24                 NIC2:192.168.10.254/24 
                       GW:192.168.0.254                      GW:192.168.0.254
                        
                               /                                  \
                              /                                    \
                             /                                      \
                        Swithcher 1                             Swithcher 2
                            |                                        |
                            |                                        |
                            |                                        |

                          PC...                                     PC...
                        192.168.5.24                              192.168.10.24
                     GW:192.168.5.254                           GW:192.168.10.254 
                     
# 設定路由服務的軟體套件

下載完套件，在環境中安裝套件後，
軟體中德 daemon 功能會更新核心的路由規則，RIP daemon 則是在向附近的其他 Router 溝通協調路由規則的傳送與否。

當得到回應，會自動在路由表建構出新的 Route Entry!

# 動態路由的設定

Router 3

    1.在此路由器上啟動軟體。
    2.給予路由器主機名稱。（DNS）
    3.配置密碼。
    4.使密碼生效。
    5.將軟體得到的資訊儲存到log檔中。
    6.下指令 netsate 檢視本機介面狀態。
    7.下軟體內建指令 sh ip route 檢視路由規則。
    
terminal in R3

    linux.R3> show ip route
    Codes: K - kernel route, C - connected, S - static, R - RIP, O - OSPF,
           I - ISIS, B - BGP, > - selected route, * - FIB route
           
GW

           K>* 0.0.0.0/0 via 192.168.0.254, eth0  
           
LAN

           C>* 192.168.0.0/24 is directly connected, eth0
    
    
Protected LAN

           C>* 192.168.10.0/24 is directly connected, eth1
   


# 手動增加額外的靜態路由

terminal in R3

    linux.R3> show ip route
    Codes: K - kernel route, C - connected, S - static, R - RIP, O - OSPF,
           I - ISIS, B - BGP, > - selected route, * - FIB route

    S>* 10.0.0.0/24 [1/0] is directly connected, eth0
    C>* 192.168.0.0/24 is directly connected, eth0

# 手動設定動態路由的前置作業

terminal in R3

    1.在此路由器上啟動軟體 ripd。
    2.給予路由器主機名稱。（DNS）
    3.配置密碼。
    4.使密碼生效。
    5.下指令 route rip 藉此啟動此路由功能。
    6.下指令 network [ip/prefix] 藉此對區域網域進行監聽工作。
    7.下指令 network [if] 針對此介面進行監聽。
    8.重複 6-7 對個別區域網路進行 rip 路由規則的設定。
    9. logstdout 直接輸出。

# R2 的設定

與 R3 相同，除了 DN 和 IP/prefix 不同以外。


# 對此架構中的 R2 、R3 下展示結果的指令

     #telnet localhost [port]
     #sh ip route
     
     >>>
     
     Codes: K - kernel route, C - connected, S - static, R - RIP, O - OSPF,
       B - BGP, > - selected route, * - FIB route

      K>* 0.0.0.0/0 via 192.168.0.254, eth0
      C>* 127.0.0.0/8 is directly connected, lo
      C>* 192.168.0.0/24 is directly connected, eth0
      C>* 192.168.10.0/24 is directly connected, eth1
  
RIP 

      R>* 192.168.5.0/24 [120/2] via 192.168.0.200, eth0, 00:06:48 <--- 出現 RIP 規則的更新結果。
     
