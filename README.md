# advent_of_code_2021
My solutions (all in the form of Python one-liners) for the Advent of Code 2021 Challenges

Note: These have NOT been optimized (with a few exceptions). The goal was to solve every challenge in one line, without investing an absurd amount of time.
Note on the Note: These are meant to be run from the command-line. (Hence the 'python -c') String formatting and quotation-mark-escaping is consistent with PowerShell syntax; may need to be adjusted for other environments

## Day 1

###	Part 1

```
python -c "print(sum(map(lambda x, y: int(y > x), depths:=[int(depth) for depth in open('input.txt').readlines()],depths[1:])))'
```

###	Part 2

```
python -c "print(len([1 for depths in [[*map(int,open('input.txt'))]] for i in range(1,len(depths)) if sum(depths[i:i+3]) > sum(depths[i-1:i+2])]))"
```	
  
### Combo

```
python -c "for x in (1,3): print(len([1 for depths in [[*map(int,open('input.txt'))]] for i in range(1,len(depths)) if sum(depths[i:i+x]) > sum(depths[i-1:i+(x-1)])]))"
```

## Day 2

###	Part 1

```    
python -c "[print(sum((f:=lambda char:[int(val) for key,val in cmdLst if key[0]==char])('f'))*(sum(f('d'))-sum(f('u')))) for cmdLst in [[line.split(' ') for line in open('input.txt')]]]"
```
   
###	Part 2

```
python -c "[print((f:=lambda char,i:sum([int(val) for key,val in cmdLst[:i] if key[0]==char]))('f',len(cmdLst)) * sum([int(cmdLst[i][1])*(f('d',i)-f('u',i)) for i in range(len(cmdLst)) if cmdLst[i][0][0]=='f'])) for cmdLst in [[line.split(' ') for line in open('input.txt')]]]"
```
   
## Day 3 

###	Part 1
   
```
python -c "[print((func:=lambda f:int(''.join([str (int(f((idxSums:=[sum([int(bStrLst[idx]) for bStrLst in bStrLsts if idx in bStrLst]) for idx in range(1+maxIdx)])[i]>(len(bStrLsts)/2)))) for i in range(1+maxIdx)]),2))(lambda x:x)*func(lambda x:not(x))) for bStrLsts in [[{i:b for i,b in [*enumerate(bstr.strip())]} for bstr in open('input.txt')]] for maxIdx in [max([i for bStrLst in bStrLsts for i in bStrLst.keys()])]]"
```
   
###	Part 2

```
python -c "[print((recursiveLambda:=lambda lstOfBstrs, idx, boolLambda: int(''.join(result[0].values()),2) if len((result:=[bstr for bstr in lstOfBstrs if bstr[idx]==str(int(boolLambda((idxSums:=[sum([int(bstr[idx]) for bstr in lstOfBstrs if idx in bstr]) for idx in range(1+maxIdx)])[idx]>=(len(lstOfBstrs)/2))))]))==1 else recursiveLambda(result,idx+1,boolLambda))(bStrLsts,0,lambda x:x)*recursiveLambda(bStrLsts,0,lambda x:not(x))) for bStrLsts in [[{i:b for i,b in [*enumerate(bstr.strip())]} for bstr in open('input.txt')]] for maxIdx in [max([i for bStrLst in bStrLsts for i in bStrLst.keys()])]]"
```

## Day 4

###	Part 1

```
python3 -c "[print((rfunc:=lambda idx:sum([num for num in winner[0] if num not in seq[:idx]])*seq[idx-1] if len((winner:=[card for card in cards if any([all([num in seq[:idx] for num in group]) for group in [[card[i] for i in idxset] for idxset in bingoIndices]])]))>0 else rfunc(idx+1))(5)) for contents in [open('input.txt').read().split('\n\n')] for seq in [[*map(int,contents[0].split(','))]] for cards in [[[*map(int,card.split())] for card in contents[1:]]] for bingoIndices in [[[*range(i,i+5)] for i in range(0,21,5)]+[[*range(i,i+21,5)] for i in range(0,5)]]]"
```
      
###	Part 2

```
python -c "[print((rfunc:=lambda idx, remaining:sum([num for num in winners[0] if num not in seq[:idx]])*seq[idx-1] if len((winners:=[card for card in remaining if any([all([num in seq[:idx] for num in group]) for group in [[card[i] for i in idxset] for idxset in bingoIndices]])]))>0 and len(remaining)==1 else rfunc(idx+1, [card for card in remaining if card not in winners]))(5, cards)) for contents in [open('input.txt').read().split('\n\n')] for seq in [[*map(int,contents[0].split(','))]] for cards in [[[*map(int,card.split())] for card in contents[1:]]] for bingoIndices in [[[*range(i,i+5)] for i in range(0,21,5)]+[[*range(i,i+21,5)] for i in range(0,5)]]]"
```

## Day 5
    
###	Part 1

```
python -c "[print(len(set([pt for pt in allpts if allpts.count(pt)>1]))) for ptsets in [[sorted([*map(lambda pt:[*map(int,pt.split(','))],pts)]) for line in [*map(str.strip,open('input.txt').readlines())] for pts in [line.split(' -> ')]]] for lnsets in [[[[pset[0][0],y] for y in range(pset[0][1],pset[1][1]+1)] if pset[0][0]==pset[1][0] else ([[x,pset[0][1]] for x in range(pset[0][0],pset[1][0]+1)] if pset[0][1]==pset[1][1] else []) for pset in ptsets]] for allpts in [[tuple(pt) for lnset in lnsets for pt in lnset]]]"
```

###	Part 2

```
python -c "[print(len(set([pt for pt in allpts if allpts.count(pt)>1]))) for ptsets in [[sorted([*map(lambda pt:[*map(int,pt.split(','))],pts)]) for line in [*map(str.strip,open('input.txt').readlines())] for pts in [line.split(' -> ')]]] for lnsets in [[[[x,int(ptset[0][1]+((ptset[1][1]-ptset[0][1])/(ptset[1][0]-ptset[0][0]))*(x-ptset[0][0]))] for x in range(ptset[0][0],ptset[1][0]+1)] if ptset[0][0]!=ptset[1][0] else [[ptset[0][0],y] for y in range(ptset[0][1],ptset[1][1]+1)] for ptset in ptsets ]] for allpts in [[tuple(pt) for lnset in lnsets for pt in lnset]]]"
```

## Day 6

###	Part 1

```    
python -c "print((f:=lambda fishcounts,daynum:sum(newcounts.values()) if ((newcounts:={num:(fishcounts[num+1] if num<8 else 0)+(fishcounts[0] if num in (6,8) else 0) for num in range(0,9)}) and daynum==1) else f(newcounts,daynum-1))({num:(initFish:=[int(num) for num in open('input.txt').read().split(',')]).count(num) for num in range(0,9)},80))"
```

###	Part 2

```
python -c "print((f:=lambda fishcounts,daynum:sum(newcounts.values()) if ((newcounts:={num:(fishcounts[num+1] if num<8 else 0)+(fishcounts[0] if num in (6,8) else 0) for num in range(0,9)}) and daynum==1) else f(newcounts,daynum-1))({num:(initFish:=[int(num) for num in open('input.txt').read().split(',')]).count(num) for num in range(0,9)},256))"
```
