version 12.1
no service pad                                                                  
service timestamps debug uptime                                                 
service timestamps log uptime                                                   
no service password-encryption                                                  
!                                                                               
hostname SDN-Switch                                                             
!                                                                               
!                                                                               
ip subnet-zero                                                                  
!                                                                               
no ip domain-lookup                                                             
!                                                                               
spanning-tree mode pvst                                                         
no spanning-tree optimize bpdu transmission                                     
spanning-tree extend system-id                                                  
!                                                                               
!                                                                               
!                                                                               
!                                                                               
interface FastEthernet0/1                                                       
!                                                                               
interface FastEthernet0/2                                                       
!                                                                               
interface FastEthernet0/3                                                       
!                                                                               
interface FastEthernet0/4                                                       
!                                                                               
interface FastEthernet0/5                                                       
!                                                                               
interface FastEthernet0/6                                                       
!                                                                               
interface FastEthernet0/7                                                       
!                                                                               
interface FastEthernet0/8                                                       
!                                                                               
interface FastEthernet0/9                                                       
!                                                                               
interface FastEthernet0/10                                                      
!                                                                               
interface FastEthernet0/11                                                      
!                                                                               
interface FastEthernet0/12                                                      
!                                                                               
interface FastEthernet0/13                                                      
!                                                                               
interface FastEthernet0/14                                                      
!                                                                               
interface FastEthernet0/15                                                      
!                                                                               
interface FastEthernet0/16                                                      
!                                                                               
interface FastEthernet0/17                                                      
!                                                                               
interface FastEthernet0/18                                                      
!                                                                               
interface FastEthernet0/19                                                      
!                                                                               
interface FastEthernet0/20                                                      
!                                                                               
interface FastEthernet0/21                                                      
!                                                                               
interface FastEthernet0/22                                                      
!                                                                               
interface FastEthernet0/23                                                      
!                                                                                                                                                            
interface GigabitEthernet0/1                                                    
!                                                                               
interface GigabitEthernet0/2                                                    
!                                                                               
interface Vlan1                                                                 
 no ip address                                                                  
 no ip route-cache                                                              
 shutdown                                                                       
!                                                                                                                                                             
ip http server                                                                  
!                                                                               
line con 0                                                                      
 logging synchronous                                                            
line vty 0 4                                                                    
 login                                                                          
line vty 5 15                                                                   
 login                                                                          
!                                                                               
!                                                                               
end