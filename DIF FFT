import numpy as np
import matplotlib.pyplot as plt
import math
def bitsize(x):
    return int(math.log(len(x),2))
def bitrev(x,size):
    binary=bin(x)
    reverse=binary[-1:1:-1]
    reverse=reverse+'0'*(size-len(reverse))
    return int(reverse,2)
def mfft(x):
    l=bitsize(x)
    xrev=[0]*len(x)
    X=[0]*len(x)
    #X1=[0]*len(x)
    #X2=[0]*len(x)
    arr1=[0]*int(len(x)/2)
    arr2=[0]*int(len(x)/2)
    stage=int(math.log(len(x),2))
    for i in range(len(x)):
        xrev[i]=x[i]
    for i in range(stage):
        sum=0
        for n in range(2**(stage-i-1)):
            arr1[n]=sum
            sum=sum+1
        for n in range(2**(stage-i-1),int(len(x)/2)):
            arr1[n]=arr1[n-(2**(stage-i-1))]+2**(stage-i)
        for n in range(int(len(x)/2)):
            arr2[n]=arr1[n]+2**(stage-i-1)
        #print(f"{i+1}th stage addition indexes={arr1}")
        #print(f"{i+1}th stage subtraction indexes={arr2}")
        for n in range(int(len(x)/2)):
            X[arr1[n]]=xrev[arr1[n]]+xrev[arr2[n]]
            #X1[arr1[n]]=xrev[arr2[n]]+xrev[arr1[n]]
        #print(f"{i+1}th stage addition portion={np.round(X1,3)}")
        k=0
        w=np.exp(-1j*2*np.pi/2**(stage-i))
        for n in range(int(len(x)/2)):
            if k<2**(stage-i-1):
                X[arr2[n]]=(xrev[arr1[n]]-xrev[arr2[n]])*(w**k)
                #X2[arr2[n]]=(xrev[arr1[n]]-xrev[arr2[n]])*(w**k)
                #print(f"{i+1}th stage subtraction portion w**k={np.round(w**k,3)}")
                k=k+1
            else:
                k=0
                X[arr2[n]]=(xrev[arr1[n]]-xrev[arr2[n]])*(w**k)
                #X2[arr2[n]]=(xrev[arr1[n]]-xrev[arr2[n]])*(w**k)
                #print(f"{i+1}th stage subtraction portion w**k={np.round(w**k,3)}")
                k=k+1
        #print(f"{i+1}th stage subtraction portion={np.round(X2,3)}")
        for n in range(len(x)):
            xrev[n]=X[n]
    for i in range(len(x)):
        X[i]=xrev[bitrev(i,l)]
    return np.round(X)
x=[5,4,1,7,9,2,5,8] #Input    
print(mfft(x))    
