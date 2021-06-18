### Generate a short guid

This project shows how to generate a unique short GUID. It uses the ["HashIds" 
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

Calls to this routine must be at least 1ms apart or you'll a GUID clash. If you are using this in a tight loop, use a SLEEP to pause the loop slightly.

    Do... 
        SLEEP 1 
        Salt = DateTime.Now().ToString('ffffff')
        Hasher = *New HashIdsNet.Hashids(Salt.ToString(), 9)
    EndDo         
