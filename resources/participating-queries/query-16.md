[Click to run](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAEAIWSQQ7CIBBF13qKHzeFRBcewLM0tB2VWLCho6Lx8KLVEipGFgT48/58CJ3TlqGwQTF7DwwzXiuMp8l+ogIfECOQYyOWMUDSeVqTa5EP8z9qjBAdkfTJXODrMOV+Bi/md5Bnsg2q8Mx912oWaokCKGTQzHlFvlNBvmjel5rJaNuQ33hUEa1HtHqiE7KOhc2zkF1LVtQSK6yD1J+MUU7fCDSoteJSOaeuwqgDla3uWTRyicVCorrCR7ttAF41gdJ2J/gY/osgKRPb3W/b7WD7AGitYzhoAgAA)

```kql
print a = '								 					  		 		 								  		 		 						  		 		 							  				 			  										 								  		 		 	  		 		 		  		 		 							  		 	 					  		 	 		  		 		 					  				 			  								 						  		 		 								  		 		 						  		 		 							  		 		 		  				 			  		 	 					  										 								  										 										  		 	 								  		 	 		  		 		 					'
| extend b = split(a, '  ')
| mv-expand with_itemindex=x b
| extend c = split(b, ' ')
| mv-expand c
| extend d = strlen(c) - 1
| summarize e = strcat_array(make_list(d), "") by x
| extend f = make_string(toint(e))
| summarize g = strcat_array(make_list(f), "")
```