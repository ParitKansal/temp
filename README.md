## Schedule
Collection of multiple transitions running on same database

## Why Concurrency
- improve throughput
- resource utilization
- reduced wating time

## Problems With Concurrency 
- Recoverability problems 
- Deadlock 
- Serializability Issues

## Dirty read / Temporary Update Problem
Read the wrong value

|T1|T2|
|-|-|
|R(x)| |
|x=x+2| |
|W(x)||
||R(x)|
|failed||

## panthon Read
first value exist then it do not exist
|T1|T2|
|--|--|
|R(x)||
||R(x)|
|delete(x)||
||R(x)|

## Ureapeatable Problem
first x shows some value but at point of time it shows other value
|T1|T2|
|--|--|
|R(x)||
||R(x)|
|x = x+5||
|W(x)||
||R(x)|

## Lost Update
update get lost
|T1|T2|
|--|--|
|R(x)||
|x = x+5||
|W(x)||
||x = x + 5|
||W(x)|
||Commit|
|failed(Rollback)||


## Incorrect summary problem
|T1|T2|
|--|--|
|R(x)||
|x=x+5||
|W(x)||
||R(x)|
||R(y)|
||Sum=x+y|
||W(Sum)|
|R(y)||
|y=y+5||
|W(y)||
- Sum when T1 is exectued first and then T2 executed ≠ Sum when T2 is exectued first and then T1 executed ≠ if exectued like above

## Good Vs Bad Schedule
Good Schedule gives consistent result

## Serial Vs Non - Serial(concurrent) Schedule
<table>
        <tr>
            <th>Non - Serial</th>
            <th>Serial</th>
        </tr>
        <tr>
            <td>
                <table class="nested-table">
                    <tr>
                        <th>T1</th>
                        <th>T2</th>
                    </tr>
                    <tr>
                        <td>R(x)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>x=x+5</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>W(x)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>R(x)</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>R(y)</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>Sum=x+y</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>W(Sum)</td>
                    </tr>
                    <tr>
                        <td>R(y)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>y=y+5</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>W(y)</td>
                        <td></td>
                    </tr>
                </table>
            </td>
            <td>
                <table class="nested-table">
                    <tr>
                        <th>T1</th>
                        <th>T2</th>
                    </tr>
                    <tr>
                        <td>R(x)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>x=x+5</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>W(x)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>R(y)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>y=y+5</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>W(y)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>R(x)</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>R(y)</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>Sum=x+y</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>W(Sum)</td>
                    </tr>
                </table>
            </td>
        </tr>
    </table>


## Serializable Schedule
A concurrent Schedule which provide result as any one Serial schedule

if a Schedule S
|T1|T2|T3|
|--|--|--|
|...| | |
|...| | |
| |...| |
| | |...|
| | |...|
|...| | |
| |...| |

Total Possible Schedules = 3!
i.e. (T1, T2, T3), (T1, T3, T2), (T2, T1, T3), (T2, T3, T1), (T3, T1, T2), (T3, T2, T1)

if S ≡ S' in all possible Schedules

Then S schedule is Serializable
## Conflict Serializability
### Conflict
    Databases statements are conflicting if and only if:
    1. Both are in different transactions 
    2. Both are accessing the same data item 
    3. Atleast one of them is write operation

### Conflict Equivalent

| T1 | T2 |
|----|----|
|R(x)|    |
|    |W(x)|
|    |R(y)|
|R(z)|    |
|    |W(z)|
|R(y)|    |

- R(x)--->W(x)
- R(z)--->W(z)

| T1 | T2 |
|----|----|
|R(x)|    |
|    |W(x)|
|R(z)|    |
|    |R(y)|
|R(y)|    |
|    |W(z)|

- R(x)--->W(x)
- R(z)--->W(z)
### Conflict Serializabllty
    A schedule is called confilct serializable if it is conflict equivalent to any serial schedule. .

    Given a concurrent Schedule S.
    Find a Serial Schedule S', such that S ≅ S' (S and S' Conflict Equivalent)
    Then S is Conflict Serializable. 

<table>
        <tr>
            <th>Example</th>
            <th>Imp Points</th>
            <th>Possible Serial Schedule</th>
        </tr>
        <tr>
            <td>
                <table>
                    <tr>
                        <th>T1</th>
                        <th>T2</th>
                        <th>T3</th>
                    </tr>
                    <tr>
                        <td>R(x)</td>
                        <td></td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>W(x)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td></td>
                        <td>R(y)</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>W(y)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>R(y)</td>
                        <td></td>
                        <td></td>
                    </tr>
                </table>
            </td>
            <td>
                <img src="https://i.ibb.co/qDfhjQh/xp-Gw-Rp-Cbiyui-Dhxr.png" alt="Precedence Graph">
            </td>
            <td>
                NaN
            </td>
        </tr>
        <tr>
            <td>
                <table>
                    <tr>
                        <th>T1</th>
                        <th>T2</th>
                        <th>T3</th>
                        <th>T4</th>
                    </tr>
                    <tr>
                        <td>R(A)</td>
                        <td></td>
                        <td></td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>W(B)</td>
                        <td></td>
                        <td></td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>R(B)</td>
                        <td></td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td></td>
                        <td>R(C)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>W(A)</td>
                        <td></td>
                        <td></td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td>R(A)</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td>R(C)</td>
                        <td></td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td>W(A)</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td></td>
                        <td>W(B)</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td>R(B)</td>
                    </tr>
                    <tr>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td>W(C)</td>
                    </tr>
                </table>
            </td>
            <td>
                <img src="https://i.ibb.co/3FpHYtG/Ov-Yxvvvkvxm-Cns-Jg.png" alt="Serializability Schedule">
            </td>
            <td>
                T1 → T2 → T3 → T3
            </td>
        </tr>
    </table>

## View Serializability(≆)

    Points to Remember for evey data item
    1. Who reads from database 
    2. Who reads from other's written value 
    3. Who writes last

### View Serializabllty
    A schedule is called confilct serializable if it is view equivalent to any serial schedule.

    Given a concurrent Schedule S.
    Find a Serial Schedule S', such that S ≅ S' (S and S' View Equivalent) 
    Then S is View Serializable. 

<table>
    <tr>
        <th>Example</th>
        <th>Imp Points</th>
        <th>Possible Serial Schedule</th>
    </tr>
    <tr>
        <td>
            <table>
                <tr>
                    <td>T1</td>
                    <td>T2</td>
                    <td>T3</td>
                    <td>T4</td>
                </tr>
                <tr>
                    <td>------</td>
                    <td>------</td>
                    <td>------</td>
                    <td>------</td>
                </tr>
                <tr>
                    <td>W(X)</td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>R(X)</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>W(X)</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>W(X)</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td>W(X)</td>
                </tr>
            </table>
        </td>
        <td>
            <ul>
                <li>T4 write last</li>
                <li>T2 read after T1 write</li>
            </ul>
            <img src="https://i.ibb.co/QfcmzF5/ue-IGflov-Avbm-Yoy-K.png" alt="Image">
        </td>
        <td>
            <ul>
                <li>T3 → T1 → T2 → T4</li>
                <li>T1 → T3 → T2 → T4</li>
                <li>T1 → T2 → T3 → T4</li>
               <li>Check each Schedule</li>
            </ul>
        </td>
    </tr>
</table>

## Recoverable Schedule 
    When no any committed transaction should be rolled back.
<table>
    <tr>
       <th>Non-Recoverable Schedule</th>
       <th>Recoverable Schedule</th>
    </tr>
    <tr>
       <td>
         <table>
            <tr>
               <th>T1</th>
               <th>T2</th>
            </tr>
            <tr>
               <td>R(x)</td>
               <td></td>
            </tr>
            <tr>
               <td>x = x + 2</td>
               <td></td>
            </tr>
            <tr>
               <td>W(x)</td>
               <td></td>
            </tr>
            <tr>
               <td></td>
               <td>R(x)</td>
            </tr>
            <tr>
               <td></td>
               <td>x = x + 5</td>
            </tr>
            <tr>
               <td></td>
               <td>W(x)</td>
            </tr>
            <tr>
               <td></td>
               <td></td>
            </tr>
            <tr>
               <td></td>
               <td>Commit</td>
            </tr>
            <tr>
               <td>failed</td>
               <td></td>
            </tr>
         </table>
       </td>
       <td>
         <table>
            <tr>
               <th>T1</th>
               <th>T2</th>
            </tr>
            <tr>
               <td>R(x)</td>
               <td></td>
            </tr>
            <tr>
               <td>x = x + 2</td>
               <td></td>
            </tr>
            <tr>
               <td>W(x)</td>
               <td></td>
            </tr>
            <tr>
               <td></td>
               <td>R(x)</td>
            </tr>
            <tr>
               <td></td>
               <td>x = x + 5</td>
            </tr>
            <tr>
               <td></td>
               <td>W(x)</td>
            </tr>
            <tr>
               <td>Commit</td>
               <td></td>
            </tr>
            <tr>
               <td></td>
               <td>Commit</td>
            </tr>
         </table>
       </td>
    </tr>
</table>

## Types of Rollback
<table>
    <tr>
        <th>Cascading Recoverable Rollback</th>
        <th>Cascadeless Recoverable Rollback</th>
    </tr>
    <tr>
        <td>
            <table>
                <tr>
                    <th>T1</th>
                    <th>T2</th>
                    <th>T3</th>
                </tr>
                <tr>
                    <td>R(x)</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td>x = x + 1</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td>W(x)</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>R(x)</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>x = x + 2</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>W(x)</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>R(x)</td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>x = x + 3</td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>W(x)</td>
                </tr>
                <tr>
                    <td>Commit</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>Commit</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>Commit</td>
                </tr>
            </table>
        </td>
        <td>
            <table>
                <tr>
                    <th>T1</th>
                    <th>T2</th>
                    <th>T3</th>
                </tr>
                <tr>
                    <td>R(x)</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td>x = x + 1</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td>W(x)</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td>Commit</td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>R(x)</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>x = x + 2</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>W(x)</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td>Commit</td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>R(x)</td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>x = x + 3</td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>W(x)</td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td>Commit</td>
                </tr>
            </table>
        </td>
    </tr>
</table>

