# 算法天梯：Day 7
这题考验的不是筒子们的算法功底，感觉更像是数学，或者说映射  
我们举个例子，就以5个数字为例  
1 2 3 4 5 -> 1  
1 2 3 5 4 -> 2 (1->2,4和5互换)  
1 2 4 3 5 -> 3 (2->3,3和4互换,3和5排序)  
1 2 4 5 3 -> 4 (3->4,3和5互换)  
1 2 5 3 4 -> 5 (4->5,4和5互换,3和4排序)  
1 2 5 4 3 -> 6 (5->6,3和4互换)  
1 3 2 4 5 -> 7 (6->7,2和3互换,2、4、5排序)  
所以能看出什么？每次+1都伴随着一个交换和一次排序（没写排序的是因为后面其实是1个元素的排序）  
交换是较小数下标最大且较大数的数值最小的顺序组（即按从小到大排列的两个数）  
排序是交换后从原较小数的下标到最后的排序，那么逻辑就很清楚了  
上代码  
```c++
int main(){
    int n,add;
    std::cin>>n>>add;
    int a[n];
    //输入，不做解释
    for(int i=0;i<n;++i){
        std::cin>>a[i];
    }
    int count=0;
    for(int i=n-1;i>0&&count<add;--i){//从后往前找下标最大的较小数
        if(a[i-1]<a[i]){//其实只要判断相邻两数即可，只要相邻的数一直是逆序整体一定逆序
            int min=i;
            for(int j=i;j<n;++j){//找后面的最小值，没什么好说的
                if(a[j]<a[min]&&a[j]>a[i-1]){
                    min=j;
                }
            }
            int temp=a[i-1];
            a[i-1]=a[min];
            a[min]=temp;
            sort(a,i,n-1);
            ++count;
            i=n;
        }
    }
    for(int i=0;i<n-1;++i){
        std::cout<<a[i]<<" ";
    }
    std::cout<<a[n-1]<<std::endl;
    return 0;
}