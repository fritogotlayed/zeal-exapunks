# Hardware Hacks

TODO: Include other #FOO registers and their behavior.

## Highway Signs

Writing to a highway sign involves a series of three-number packets written to
#DATA. The first number is the row (starting at 0), the second is the column
(also starting at 0), and the third corresponds to the character you want to
display.

### #DATA

> COPY **#DATA** 0 ; row  
COPY **#DATA** 0 ; column  
COPY **#DATA** 1 ; datum

The **#DATA** register allows one to write information to the highway sign.
Note that the register accepts data three (3) times before a single character
is written.

### #CLRS

> COPY **#CLRS** 0 ; any datum works

The **#CLRS** register will clear the sign of any text if you write anything to
it.

### Common Character Table

| datum | result  | datum | result  | datum | result  | datum | result  | datum | result  | datum | result  | datum | result  | datum | result  |
|-------|---------|-------|---------|-------|---------|-------|---------|-------|---------|-------|---------|-------|---------|-------|---------|
| 0     | (space) | 5     | E       | 10    | J       | 15    | O       | 20    | T       | 25    | Y       | 30    | 3       | 35    | 8       |
| 1     | A       | 6     | F       | 11    | K       | 16    | P       | 21    | U       | 26    | Z       | 31    | 4       | 36    | 9       |
| 2     | B       | 7     | G       | 12    | L       | 17    | Q       | 22    | V       | 27    | 0       | 32    | 5       | 37    | .       |
| 3     | C       | 8     | H       | 13    | M       | 18    | R       | 23    | W       | 28    | 1       | 33    | 6       | 38    | ?       |
| 4     | D       | 9     | I       | 14    | N       | 19    | S       | 24    | X       | 29    | 2       | 34    | 7       | 39    | !       |

## Digicash Point-Of-Sale Systems

### Customer Database

The customer database (usually file 200) stores a list of customers with three
values for each customer: The customer ID, dollars owed, and cents owed.

### Transaction Log

The transaction log (usually, you guessed it, file 201) stores a list of
transactions with four values for each transaction: The date, the customer ID,
the dollars paid, and the cents paid.

## Legacy Storage Systems

### Tape storage

An EXA-accessable tape storage system typically consists of one host per tape
unit, with each unit's tape mounted as a file that can be read and written.
Each tape contains zero or more backup entries. The data for these entries
starts at the beginning of the tape and is concatenated sequentially, making it
impossible to tell which data belongs to which backup entry.

Metadata for the entries is stored at the end of the file in three-value
triplets. The first value is the entry's name, the second value is the offset
in the data stream where the entry's data starts (0 = beginning), and the third
value is the length of the entry.

For example, to get the data for an entry with metadata "SECRET, 3, 4", you'd
go to the beginning of the file, skip the first three values, then read off the
next four values (in order).

1234, 4567, 9012, **3456**, **7890**, **1234**, **56787**, 0, 0,
BORING, 0, 3, SECRET, 3, 4

### Hard drive arrays

Within the array, each drive is typically mapped to its own host and contains
up to 10 files, starting with file ID 200 up to file ID 209. Each file will
contain 100 values divided into 10 checks of 10 values each.

The first file (200) in the first drive should contain a table of all backup
entries contained in the drive array. Each entry consists of the entry's name
followed by the addresses of the chunks storing that entry's data. A chunk
address is a number between 100 and 999 that points to a chunk located
somewhere in the drive array. The first digit indicates the drive that contains
the chunk (1-9), the second digit indicates the file that contains the chunk
(0-9, mapping to files 200-209), and the final digit indicates the location of
the chunk within the target file (0-9, mapping to offsets 0 through 90).

For example, to retrieve chunk 527, you'd access drive 5, grab file 202, seek
to offset 70, and read the next 20 values (the size of a chunk).

## Network Exploration

### Workhouse

### Equity First Bank