#### storage slot for mapping builds like ?

1 . concatenate the key associated with the value and the mapping variable storage slot (base slot 0
2 . hash the concatenated result 

##### Formula for the above steps 
```diff
byte32storageSlot=keccak256(byte32(key)⊕byte32(baseSlot));
where ⊕ means concatenate
```
under the hood the key and base slot are both stored as 256 bit (32 bytes) value. when they are concatenated together they are a 64 bytes value.

---

nested mapping is a mapping within another mapping 
usecase : storing balances of different tokens for a  specific address 

storage calcuation for nested mapping 

- suppose there 2 keys : key 1 : key 2

initialHash = keccack256(key 1 [concatinate] baseSlot[where we want to put out data])
then add one more step :
slot = keccack256(key2 [concatinate] initialHash)

this completes an nested mapping 

----

#### BYTES 

short bytes is <= 31 : stored entirely in the base slot including its length number of bytes * 2
long bytes > 31 bytes the base slot stores the length number of bytes * 2 + 1. and the actual data is stored in consecutive slots starting from the keccack256 hash of the base slot. 
