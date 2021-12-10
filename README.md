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

## Day 7

### Part 1

```
python -c "print(sum(map(lambda x:abs(x-l[len(l)//2]),l:=sorted([*map(int,open('input.txt').read().split(','))]))))"
```

### Part 2

```
python -c "print(min([sum(map(lambda x:(n:=abs(x-int(sum(l)/len(l))+passedval))*(n+1)//2,(l:=[*map(int,open('input.txt').read().split(','))]))) for passedval in (0,1)]))"
```

## Day 8

### Part 1

```
python -c "print(len([digit for output in [line.split('|')[-1].split() for line in open('input.txt').readlines()] for digit in output if len(digit) in (2,4,3,7)]))"
```

### Part 2

```
python -c "print(sum(int(''.join([{42:'0',17:'1',34:'2',39:'3',30:'4',37:'5',41:'6',25:'7',49:'8',45:'9'}[sum([entry[0].count(l) for l in digit])] for digit in entry[1].split()])) for entry in [line.split('|') for line in open('input.txt').readlines()]))"
```

## Day 9

### Part 1

```
python -c "print(sum(low:=(lambda hmap:[hmap[x][y] for x in range(len(hmap)) for y in range(len(hmap[x])) if all([hmap[x][y]<hmap[i][j] for i,j in [(x-1,y),(x+1,y),(x,y-1),(x,y+1)] if i in range(0,len(hmap)) and j in range(0,len(hmap[x]))])])([[*map(int,line.strip())] for line in open('input.txt').readlines()]))+len(low))"
```

### Part 2

```
python -c "print(eval('*'.join([*map(lambda basin:str(len(basin)),sorted((lambda hmap:[(trace:=lambda oldpts,currentpts:set(oldpts+currentpts) if len(newpts:=[(c,d) for a,b in currentpts for c,d in [(a-1,b),(a+1,b),(a,b-1),(a,b+1)] if c in range(0,len(hmap)) and d in range(0,len(hmap[a])) if hmap[c][d] in range(hmap[a][b]+1,9)])==0 else trace(oldpts+currentpts,newpts))([],[(x,y)]) for x in range(len(hmap)) for y in range(len(hmap[x])) if all([hmap[x][y]<hmap[i][j] for i,j in [(x-1,y),(x+1,y),(x,y-1),(x,y+1)] if i in range(0,len(hmap)) and j in range(0,len(hmap[x]))])])([[*map(int,line.strip())] for line in open('input.txt').readlines()]), key=lambda val:len(val))[-3:])])))"
```
