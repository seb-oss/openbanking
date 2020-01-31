# Status Code
 
Status Code       | Status Message
------------------|----------------------
A0         | Success             
A1         | Pending             
A2         | Redirect            
A3         | Cancelled by user   
A4         | OK, needs extra verification
A5         | More data available 
A6         | Not ready           
 
 
Status Code       | Message         
------------------|----------------------
D0         | Phone number missing, The PSU should contact their bank
 
 
Status Code       | Message         
------------------|----------------------
E0         | Parallel invocation
E1         | Service Unavailable
E2         | Limit exceeded for erroneous OTPs
E3         | Limit for number of OTPs exceeded   
E4         | Validity Time for OTP expired
E5         | OTP invalid- a newer exists 
E6         | Wrong OTP           
 
 
 
Status Code       | Message         
------------------|----------------------
F0         | Message from BankID backend that forced us to interrupt collect calls   
F1          | Order reference was not returned from BankID backend   
F2          | Unhandled exception    
F3          | Session does not exist   
F4          | Missing attribute in session   
F5          | Invalid synchronizer token   
F6          | Redirect called, but user was not authenticated   
F7          | Validation error   
F8          | Contact the bank
F9          | Client did not follow the process   
FA          | Backend error   
FB          | Invalid OTP   
FD          | Device not accepted    
FE          | Device warning   
FF          | Other error   
 
