### Generate a short guid

This project shows how to generate a unique short GUID. It uses the ["HashId" 
library.](https://hashids.org/net/)

This code always returns a 10-character short GUID that starts with 'X'. This can be used to generate unique file names for the IBM i. 

    BegFunc GetShortGuid Type(*String) 
        DclFld Hasher Type(HashidsNet.Hashids) 
        DclFld Salt Type(*Integer4) 

        DclConst SHORT_GUID_LENGTH Value(9) 

        Salt = DateTime.Now().ToString('ffffff')
        Hasher = *New HashIdsNet.Hashids(Salt.ToString(), 9)

        LeaveSr ('X' + Hasher.Encode(Salt)).ToUpper()
    EndFunc 
