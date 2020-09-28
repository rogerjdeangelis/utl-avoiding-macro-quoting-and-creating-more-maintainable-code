# utl-avoiding-macro-quoting-and-creating-more-maintainable-code
Avoiding macro quoting and creating more maintainable code?  
    Avoiding macro quoting and creating more maintainable code?                                         
                                                                                                        
    * Perhaps the code below is more maintainable;                                                      
                                                                                                        
    %let list = %str(%')%qsysfunc(prxchange(%str(s/\s|,/','/),-1,%superq(mvar)))%str(%');               
    %let list = %unquote(&list);                                                                        
                                                                                                        
    github                                                                                              
    https://tinyurl.com/yxlpzqgu                                                                        
    https://github.com/rogerjdeangelis/utl-avoiding-macro-quoting-and-creating-more-maintainable-code   
                                                                                                        
    SAS Forum                                                                                           
    https://tinyurl.com/y3uxoo8f                                                                        
    https://communities.sas.com/t5/SAS-Programming/quotes-to-macro-variable-string/m-p/687077           
                                                                                                        
    /*                   _                                                                              
    (_)_ __  _ __  _   _| |_                                                                            
    | | `_ \| `_ \| | | | __|                                                                           
    | | | | | |_) | |_| | |_                                                                            
    |_|_| |_| .__/ \__,_|\__|                                                                           
            |_|                                                                                         
    */                                                                                                  
                                                                                                        
    %let mvar=aaaaa bbbbb ccccc zzzzz;                                                                  
                                                                                                        
    /*           _               _                                                                      
      ___  _   _| |_ _ __  _   _| |_                                                                    
     / _ \| | | | __| `_ \| | | | __|                                                                   
    | (_) | |_| | |_| |_) | |_| | |_                                                                    
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                   
                    |_|                                                                                 
    */                                                                                                  
                                                                                                        
    %put &=lst;                                                                                         
                                                                                                        
    LST="aaaaa","bbbbb","ccccc","zzzzz"                                                                 
                                                                                                        
    /*         _       _   _                                                                            
     ___  ___ | |_   _| |_(_) ___  _ __                                                                 
    / __|/ _ \| | | | | __| |/ _ \| `_ \                                                                
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                               
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                               
                                                                                                        
    */                                                                                                  
                                                                                                        
    %symdel lst / nowarn;                                                                               
                                                                                                        
    %dosubl('                                                                                           
             data _null_;                                                                               
               length list $96;                                                                         
               retain mvar "&mvar";                                                                     
               do i= 1 to countc(mvar," ") + 1;                                                         
                  list=catx(",",list,quote(scan(mvar,i," ")));                                          
                  call symputx("lst",list);                                                             
               end;                                                                                     
             run;quit;                                                                                  
            ');                                                                                         
                                                                                                        
    %put &=lst;                                                                                         
                                                                                                        
    LST="aaaaa","bbbbb","ccccc","zzzzz"                                                                 
                                                                                                        
                                                                                                        
