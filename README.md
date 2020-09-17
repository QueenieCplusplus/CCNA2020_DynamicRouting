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


