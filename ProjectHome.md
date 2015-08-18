Here's a little database library I created that has been very useful for me, so I thought I would share. It makes use of the Arduino's EEPROM memory to store records in a table. I kept it simple to keep it small. You will have to spin your own locate and other functions like validation.

How to use in a nutshell:

  * include Db.h and EEPROM.h
  * declare an instance of DB, db
  * define a structure for your records
  * pick an address in EEPROM for the table to start
  * make a little sketch that creates the table by calling db.create(address,sizeof(myRecStruct))
  * in your application's sketch open the table with db.open(address)
  * use the define DB\_REC to cast your structure as a byte pointer when passing it as a parameter for write and read operations, this helps make the code more readable.

---

## Example ##
```
#include <EEPROM.h>
#include <DB.h>
DB db;
#define MY_TABLE 128
struct MyRec {
  byte id;
  char name[9];
  int    val;
} myrec;

  db.create(MY_TBL,sizeof(myrec));
  myrec.id = 1;
  myrec.name[0]='O';
  myrec.name[1]='N';
  myrec.name[2]='E';
  myrec.name[30=0;
  db.append(DB_REC myrec);
 ...

  db.open(MY_TBL);
  for (int i=1;i<db.nRecs();i++)
  {
    db.read(i, DB_REC myrec);
    Serial.println(myrec.name);
  }
```