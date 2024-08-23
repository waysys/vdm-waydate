# CompletedMonths - computations involving months and years

## Definiton: Completed Months 

Given a number of months and a year on or after January, 1601, the completed months are the number of months from January, 1601, until (but not including) the specified month and year.

```vdm-sl
firstMonthYear = create(1, 1601)
completedMonths(firstMonthYear) = 0
for (month, year) where 1 <= month < 12,
    completedMonths(month + 1, year) = completedMonths(month, year) + 1  
for (month, year) where month = 12,  
    completedMonths(month + 1, year) = completedMonths(1, year+1)
```

## Function

```vdm-sl
Minyear = 1601

completedMonths: MonthYear -> int 
completedMonths(monthYear) == 
    let
        month = monthToInt(monthYear.month),
        year = yearToInt(monthYear.year)
    in
        12 * (year - MinYear) + (month - 1);
```

## Proof Obligations

### Proof Oblication 1
#### Given:
```vdm-sl
firstMonthYear = create(1, 1601)
```
#### Prove:
```vdm-sl
completedMonths(firstMonthYear) = 0
```

### Proof Obligation 2
#### Given:
```vdm-sl
1 <= month < 12 
```
#### Prove:
```vdm-sl
completedMonths(month + 1, year) = completedMonth(month, year) + 1
```
### Proof Obligation 3
#### Given:
```vdm-sl
month = 12
```
#### Prove:
```vdm-sl
completedMonths(month + 1, year) = completedMonth(1, year + 1)
```

## Proofs

| **Proof** | Proof Obligation 1|
| --- | ---                     |
|     | completedMonths(create(1, 1601) |
| =   | <substitution in function>    |
|     | 12 * (1601 - 1601) + (1 - 1) |
| =   | <reduction> |
|     | 12 * 0 + 0 |
| =   | <reduction> |
|     | 0 |

| **Proof** | Proof Obligation 2 |
| --- | --- |
|     | coompletedMonths(month + 1, year) |
| =   | <substitution in function> |
|     | 12 * (year - MinYear) + (month + 1 - 1) |
| =   | <rearrangement> |
|     | (12 * (year - MinYear) + (month - 1) + 1 |
| =   | <substitution> |
|     | completedMonths(month, year) + 1

| **Proof** | Proof Obligation 3 |
| --- | --- |
|     | completedMonths(month + 1, year) |
| =   |   <substitution>
|     | 12 * (year - MinYear) + (month + 1 - 1) |
| =   |   <rearrangement and month = 12> |
|     | 12 * (year + 1 - MinYear) + (1 - 1) |
| =   |   <substitution> |
|     | completedMonths(1, year + 1)



