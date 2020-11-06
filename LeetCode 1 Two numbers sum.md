双指针做法，暴力遍历：


```python
%%time
def findindex(list,target):
    result=[0,0]
    length=len(list)
    for i in range(0,length):
        for j in range(i+1,length):
            if list[i]+list[j]==target:
                result[0]=i
                result[1]=j
                print(result)
my_list=[11,25,36,42,57]
target=67
findindex(my_list,target)
```

    [1, 3]
    Wall time: 984 µs



Hash做法：


```python
%%time
def hashfindindex(list,target):
    mapping={}
    for i in range(len(list)):
        diff=target-list[i]
        if diff in mapping.keys():
            return [mapping[diff],i]
        else:
            mapping[list[i]]=i
my_list=[11,25,36,42,57]
target=67
hashfindindex(my_list,target)
```

    Wall time: 0 ns
    
    [1, 3]



