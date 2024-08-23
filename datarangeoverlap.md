# DataRange - overlap

## Function

```vdm-sl
overlaps: DateRange * DateRange -> bool
overlaps(range1, range2) ==
   if WayDate`before(range1.last, range2.first) then false
   elseif WayDate`after(range1.first, range2.last) then false
   else true;
```

## Proof Obligation 1

If two ranges overlap, then there is a date that is in both ranges.  

overlap(range1, range2) = exists date & inRange(range1, date) and inRange(range2, date)

## Proof Obligaton 2

If they do not overlap,
then there is no date that is in both ranges.

not overlap(range1, range2) = forall date & not inRange(range1, date) or not inRange(range2, date)

## Proof 1 by cases

```text
|     | overlap(range1, range2) = true
|  =  |   <definition of overlap>          
|     | range1.first <= range2.last and range2.first <= range1.last

Case    assume range2.first >= range1.first and date = range2.first
|  =  |  <introduce exists; range2.first is in range2 by definitoon>
|     | (exists date & range1.first <= date <= range1.last) and inRange(range2, date) 
|  =  |   <definition of inRange>
|     | exists date & inRange(range1, date) and inRange(range2, date)

Case    assume range2.first < range1.first and date = range1.first
|  =  |   <introduce exists; case assumption>
|     | exists date & range2.first < date <= range2.last
|  =  |   <definition of inrange; range2.first is in range2 by definitoon>
|     | exists date & inRange(range1, date) and inRange(range2, date)

|  =  |   <first and second cases>
|  =  | exists date & inRange(range1, date) and inRange(range2, date)

## Proof 2

|     | not overlao(range1, range2) and exists date & inRange(range1, date) and inRange(range2, date) 
|  =  |   <definition of overlap>
|     | range1.last < range2.first or range1.first > range2.last
|  =  |   <assumption>
|     | inRange(range1, date) and inRange(range2, date)
|  =  |   <definition of inRange>
|     | date >= range1.first and date <= range1.last and date >= range2.first and date <= range2.last
|  =  |   <case 1>
|     | date <= range1.last < range2.first and date >= range2.first
|  =  |   <contradiction>
|     | false
|  =  |   <case 2>
|     | date <= range1.first > range2.last and date <= range2.last
|  =  |   <contraditon>
|     | false
|  =  |   <both case 1 and case 2 false>
|     | not overlap(range1, range2) and not exits date & inRange(range1, date) and inRange(range2, date)
```
