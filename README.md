# CCNA2020_DynamicRouting
動態路由，由軟體輸入 route entry


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

