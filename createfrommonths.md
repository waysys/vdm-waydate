# CreateFromMonths - conversion from completed months to month and year

## Function

Create a MonthYear from the completed months.

```vdm-sl
createFromMonths: int -> MonthYear
createFromMonths(months) ==
    let
        year = intToYear(months div 12 + MinYear),
        month = intToMonth(months mod 12 + 1)
    in
        create(month, year)
pre 0 <= months and months <= MaxCompletedMonths
post isMonthYear(RESULT) and completedMonths(RESULT) = months;
```

## Proof Obligations

### Proof Obligation 1

```vdm-sl
createFromMonths(0) = mk_MonthYear(1, 1601)
```

### Proof Obligation 2

#### Given:

```vdm-sl
MaxCompleteMonths = completedMonths(mk_MonthYear(12, MaxYear))
0 <= months and months <= MaxCompletedMonths
monthYear = createFromMonths(months)
```

### Prove:

```vdm-sl
completedMonths(monthYear) = months
```

## Proofs

| **Proof** | Proof Obligation 1 |
| ---       | --- |
|           | createFromMonths(0) |
| =         |    <substitution> |
|           | year = 0 div 12 + MinYear; month = 0 mod 12 + 1 |
| =         |    <definition of createFromMonth> |
|           | year = MinYear; month = 1; create(1, MinYear) |
| =         |    <definition of create, MinYear> |
|           | mk_MonthYear(1, 1601) |

| **Proof** | Proof Obligation 2 |
| ---       | --- |
|           | createFromMonths(months) |
| =         |    <function invocation> |
|           | 