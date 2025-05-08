[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAI1V23LTMBB9tr9i32J3nKYppe3QyUsLD9xmGAr0AZhUtuVGVLY8kkIbCK98AJ/Il7C6JW7itngyjmPtrs5ZnbMZjeBixjSF85YUeNeSNVfAGi3g9VxpEXOqXYQyAS+aQi5aDRNIWk5Y80zZhDT+GQNeoxGMd0ORv7//AJGSLEBU8LFhhSgpmNuwFbiBshkthmooWoUl5y5mam4uZFpJUU/dHm7D1GYtof4+pLctaUrMxVRTwK/QW03t65eNwalNoaRoU3jsQvAFURpEg42ohISc6aFoVWC2vwsXhF+DnlE4NosKkrfnp0jzzflpmiEVUc4L38nRB5KvoZK25QtQM1YZSOWiITUrks9H2WH2NDvInmT72Tjb+5ri3pDEAZBngjt9IhzzctYQuZgi6eQRHpKS0uLE3Lg3yNeykKaSXc1Mj7BjmW+YXUiR1ThdFVh2EJ3NJCJiVZUEeBMYZzD4ogd4h0Gn3YhnR9FCNOVOKDBXVHlenepqXtdEsh/UNXcCePAF0VMrovsom1MTnNNC46GoRZ0Lrvop1+SaTjlTOnH4kdxgENgFXSkqGeEGQzj2J7vwClsC+QI9kAEpS2joDWcNhZJyVqM1ZEheEUCfoIjLTQ5xHxoXYUAp08BmkHaQLY2svhl2vmT862TDk8/pypMFa2dU9pryFDVxDS7A+ft46NoFhkvXjfa3gd5ypn1Nj2zLfbYPk06JJdxgODW8OW0Ss5AacRx3bPSeDolStM45dSrF1oKx+v3eaYXqOmcP/bKPvjlA/xxmR485x+hUzXM/SAymoHOse1fkfRfCd8JGhe/1+AG1jZXztUWdrTitdI9ssQduEthTwKlW0Ad3dywyOIJhB3QKvc4JYw/fJB7WvRLvKPxsPZbt3C5mRJICle1+VkiLg2vfltbfmbn8X0rvGfBahPF+l3R/R1Ad136DMNeRbpp6xwBseMZCC465MY5xf3MTuLy8hAjwE2FOFJnvyD3gLbwx5SIPJ7IPdsmuhodusPv2wZ2Cd+rYlejBTVeVu7tHWzBC1qrgxqbI8STemhPJug/pP7xmIhH+BwAA)

```kql
// White Space String into Kusto
let WhitespaceEncrypt = (plain:string)
{
    // 1. String → array of Unicode code-points
    print cps = unicode_codepoints_from_string(plain)
    | mv-expand cp = cps 
    | extend cpInt = toint(cp)                                 // cast once for bit-ops
    // 2. Walk the 8 bits (MSB→LSB), produce Space/Tab
    | mv-apply shift = dynamic([7,6,5,4,3,2,1,0]) on (
        extend bitVal = binary_and(                            // read the bit
                     binary_shift_right(cpInt, toint(shift)), 1)
        | extend bitChr = iff(bitVal == 1, '\t', ' ')          // *second* extend uses bitVal
        | summarize bits = strcat_array(                       // collect 8 symbols
                     make_list(bitChr), '')
      )
    | serialize 
    // 3. Join bytes, add newline delimiter
    | summarize Encoded = strcat_array(
          make_list(strcat(bits, '\n')), '')
    | project Encoded
};
let WhitespaceDecrypt = (cipher:string)
{
    // 1. Break cipher into 8-symbol lines
    print lines = split(cipher, '\n')
    | mv-expand line = lines
    | where strlen(line) == 8
    // 2. Re-assemble the byte from Space/Tab
    | mv-apply pos = dynamic([0,1,2,3,4,5,6,7]) on (
        extend bitVal = iff(substring(line, toint(pos), 1)
                            == '\t', 1, 0)
        | extend contrib = binary_shift_left(                  // shift into place
                            bitVal, 7 - toint(pos)) 
        | summarize cpInt = sum(contrib)
      )
    | serialize
    // 3. Code-points → characters → final string
    | summarize Plain = strcat_array(
          make_list(unicode_codepoints_to_string(              
                     pack_array(toint(cpInt)))), '')  
    | project Plain
};
let whiteSpace = ``` 	  	 	 
 			 	 	
 			  		
 			 	  
  	     
 		    	
 		 			 
 		 				
 			 	  
 		 	   
 		  	 	
 			  	 
  	     
 	  	 		
 			 	 	
 			  		
 			 	  
 		 				
  	     
 		 	   
 		    	
 		   		
 		 	 		
 		  	 	
 			  	 
```;
WhitespaceDecrypt(whiteSpace)
```