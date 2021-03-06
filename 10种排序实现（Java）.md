十大常用排序算法（java实现）
【前言】最近在重新研究算法，此篇博文供自己复习使用也为方便广大程序员同学！此文代码均为自己实现，通过对比经典解法校验，若有错请读者及时提出！
- 【对比分析图】首先，我们先来对比分析一下这十大排序算法的特点： 

![image](http://a3.qpic.cn/psb?/V12GFpMj3t6YfU/sRXaKfIeeR3uL*NuiXN6ieil3*NEahQCLiOeaSfUvRc!/b/dCIBAAAAAAAA&ek=1&kp=1&pt=0&bo=fAMfAnwDHwIBACc!&tl=3&vuin=2358489652&tm=1531735200&sce=60-4-3&rf=viewer_311)

![image](http://a2.qpic.cn/psb?/V12GFpMj3t6YfU/byjw65EalrAYxlh5M1eMW78l3YPXJAVwmqkcNGu6SuM!/b/dCEBAAAAAAAA&ek=1&kp=1&pt=0&bo=QwJnAUMCZwEBACc!&tl=1&vuin=2358489652&tm=1531735200&sce=50-1-1&rf=viewer_311)

（一）.冒泡排序（优化）

【题目】对于一个int数组，请编写一个冒泡排序算法，对数组元素排序。 
给定一个int数组A及数组的大小n，请返回排序后的数组。

冒泡排序，顾名思义，从下往上遍历，每次遍历往上固定一个最小值
加一个标志位，当某一趟冒泡排序没有元素交换时，则冒泡结束，元素已经有序，可以有效的减少冒泡次数。
    
    import java.util.*;

    public class BubbleSort {
        public int[] bubbleSort(int[] A, int n) {
            //冒泡排序：从后往前（从下往上）就像冒泡一样
            //用flag作为标记，标记数组是否已经排序完成
            boolean flag = true;
            //固定左边的数字
            for(int i=0; i<n-1&flag; i++){
                flag = false;
                //从后面（下面）往前（上）遍历
                for(int j=n-2;j>=i;j--){

                if(A[j]>A[j+1]){
                    swap(A,j,j+1);
                    flag = true;
                }
            }
        }

        return A;

    }
      //数组是按引用传递，在函数中改变数组起作用
        private void swap(int[] A,int i,int j){
            int temp = A[i];
            A[i] = A[j];
            A[j] = temp;
        }
    }

（二）.简单选择排序

【题目】 对于一个int数组，请编写一个选择排序算法，对数组元素排序。 
给定一个int数组A及数组的大小n，请返回排序后的数组。

1.【初始升序】：交换0次，时间复杂度为o(n); 【初始降序】：交换n-1次，时间复杂度为o(n^2)。
【特点】：交换移动数据次数少，比较次数多。
   
    import java.util.*;
    
    /**

    **/
    public class SelectionSort {
        public int[] selectionSort(int[] A, int n) {
           //简单选择排序算法,排序结果为递增数组
            //记录最小下标值
            int min=0;
            //固定左边的数字
            for(int i=0; i<A.length-1;i++){
                min = i;
                //找到下标i开始后面的最小值
                for(int j=i+1;j<A.length;j++){

                 if(A[min]>A[j]){
                     min = j;
                 }
            }
           //确保稳定排序,数值相等就不用交换
            if(i!=min){
                swap(A,i,min);
            }
        }

        return A;

    }

    //数组是按引用传递，在函数中改变数组起作用
    private void swap(int[] A,int i,int j){
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }

}

（三）.直接插入排序

【题目】对于一个int数组，请编写一个插入排序算法，对数组元素排序。 
给定一个int数组A及数组的大小n，请返回排序后的数组。

    import java.util.*;

    public class InsertionSort {
        public int[] insertionSort(int[] A, int n) {
          //用模拟插入扑克牌的思想
            //插入的扑克牌
            int i,j,temp;
            //已经插入一张，继续插入
            for(i=1;i<n;i++){

            temp = A[i];
            //把i前面所有大于要插入的牌的牌往后移一位，空出一位给新的牌
            for(j=i;j>0&&A[j-1]>temp;j--){
                A[j] = A[j-1];
            }
            //把空出来的一位填满插入的牌
            A[j] = temp;

        }
        return A;


    }
}

（四）.希尔排序

【题目】对于一个int数组，请编写一个希尔排序算法，对数组元素排序。 
给定一个int数组A及数组的大小n，请返回排序后的数组。保证元素小于等于2000。

基本思想：算法先将要排序的一组数按某个增量d（n/2,n为要排序数的个数）分成若干组，每组中记录的下标相差d.对每组中全部元素进行直接插入排序，然后再用一个较小的增量（d/2）对它进行分组，在每组中再进行直接插入排序。当增量减到1时，进行直接插入排序后，排序完成。

希尔排序法(缩小增量法) 属于插入类排序，是将整个无序列分割成若干小的子序列分别进行插入排序的方法。


    import java.util.*;

    public class ShellSort {
        public int[] shellSort(int[] A, int n) {
            //要插入的纸牌
            int temp,j,i;
            //设定增量D,增量D/2逐渐减小
            for(int D = n/2;D>=1;D=D/2){

            //从下标d开始，对d组进行插入排序
            for(j=D;j<n;j++){

                temp = A[j];
                for(i=j;i>=D&&A[i-D]>temp;i-=D){
                    A[i]=A[i-D];
                }

                A[i]=temp;
            }

        }

        return A;
    }
}

（五）.堆排序

【题目】对于一个int数组，请编写一个堆排序算法，对数组元素排序。 
给定一个int数组A及数组的大小n，请返回排序后的数组。

【堆】 1.堆是完全二叉树 2.大顶堆：每个结点的值都大于或等于其左右孩子结点的值，称为大顶堆。3.小顶堆：每个结点的值都大于或等于其左右孩子结点的值，称为小顶堆。
【完全二叉树性质5】：如果i>1,则双亲是结点[i/2]。也就是说下标i与2i和2i+1是双亲子女关系。 当排序对象为数组时，下标从0开始，所以下标 i 与下标 2i+1和2i+2是双亲子女关系。

    import java.util.*;

    public class HeapSort {
        public int[] heapSort(int[] A, int n) {
            //堆排序算法

        int i;
        //先把A[]数组构建成一个大顶堆。
        //从完全二叉树的最下层最右边的非终端结点开始构建。
        for(i=n/2-1;i>=0;i--){
            HeapAdjust(A,i,n);
        }

        //开始遍历
        for(i=n-1;i>0;i--){
            swap(A,0,i);
            //每交换一次得到一个最大值然后丢弃
            HeapAdjust(A,0,i);
        }
        return A;

    }
        //A[i]代表的是下标为i的根结点
        private void HeapAdjust(int[] A,int i,int n){
            //【注意】这里下标从0开始
            int temp;
            //存储根结点
            temp = A[i];
            //沿根结点的左右孩子中较大的往下遍历,由于完全二叉树特性 i的左子节点2i+1  i的右子节点2i+2
            for(int j=2*i+1;j<n;j=j*2+1){

                if(j<n-1&&A[j]<A[j+1]){
                    ++j;
                }

                if(temp>=A[j]){
                    break;
                }
                //将子节点赋值给根结点
                A[i] = A[j];
                //将子节点下标赋给i
                i = j;
            }
            //将存储的根结点的值赋给子节点
            A[i] = temp;

        }
        private void swap(int[] A,int i,int j){
            int temp = A[i];
            A[i]=A[j];
            A[j] = temp;

        }
    }

（六）.归并排序算法

【题目】对于一个int数组，请编写一个归并排序算法，对数组元素排序。 
给定一个int数组A及数组的大小n，请返回排序后的数组。

先用递归方法，默认排序方法为2路归并排序。看下图应该能立即理解： 
这里写图片描述
先使每个子序列有序，再将两个已经排序的序列合并成一个序列的操作。若将两个有序表合并成一个有序表，称为二路归并。
   
    import java.util.*;

    public class MergeSort {
        public int[] mergeSort(int[] A, int n) {
           //归并排序，递归做法，分而治之

            mSort(A,0,n-1);
            return A;
        }

        private void mSort(int[] A,int left,int right){
            //分而治之，递归常用的思想，跳出递归的条件
            if(left>=right){
                return;
            }
            //中点
            int mid = (left+right)/2;
            //有点类似后序遍历！
            mSort(A,left,mid);
            mSort(A,mid+1,right);

            merge(A,left,mid,right);



        }

        //将左右俩组的按序子序列排列成按序序列
        private void merge(int[] A,int left,int mid,int rightEnd){
            //充当tem数组的下标
            int record = left;
            //最后复制数组时使用
            int record2 = left;
            //右子序列的开始下标
            int m =mid+1;
            int[] tem = new int[A.length];

            //只要left>mid或是m>rightEnd，就跳出循环
            while(left<=mid&&m<=rightEnd){

                if(A[left]<=A[m]){

                    tem[record++]=A[left++];
                }else{
                    tem[record++]=A[m++];
                }

            }
            while(left<=mid){
                tem[record++]=A[left++];
            }
            while(m<=rightEnd){
                tem[record++]=A[m++];
            }
            //复制数组
            for( ;record2<=rightEnd;record2++){
                A[record2] = tem[record2];
            }

        }

    }

（七）.快速排序算法

【题目】对于一个int数组，请编写一个快速排序算法，对数组元素排序。 
给定一个int数组A及数组的大小n，请返回排序后的数组。

【基本思想】：快速排序（Quicksort）是对冒泡排序的一种改进，使用分治法（Divide and conquer）策略来把一个序列（list）分为两个子序列（sub-lists）。

【步骤为】

从数列中挑出一个元素，称为”枢轴”（pivot）。
重新排序数列，所有元素比枢轴值小的摆放在基准前面，所有元素比枢轴值大的摆在枢轴的后面（相同的数可以到任一边）。在这个分区结束之后，该枢轴就处于数列的中间位置。这个称为分区（partition）操作。
递归地（recursive）把小于枢轴值元素的子数列和大于枢轴值元素的子数列排序。

    import java.util.*;

    public class QuickSort {
        public int[] quickSort(int[] A, int n) {
            //快速排序

        qSort(A,0,n-1);

        return A;

    }
    public void qSort(int[] A,int left,int right){

         //枢轴
        int pivot;
        if(left<right){

            pivot = partition(A,left,right);

            qSort(A,left,pivot-1);
            qSort(A,pivot+1,right);

        }      

    }

    //优化选取一个枢轴，想尽办法把它放到一个位置，使它左边的值都比它小，右边的值都比它大
    public int partition(int[] A,int left,int right){

        //优化选取枢轴，采用三数取中的方法
        int pivotKey = median3(A,left,right);
        //从表的俩边交替向中间扫描
        //枢轴用pivotKey给备份了
        while(left<right){
           while(left<right&&A[right]>=pivotKey){
               right--;
           }
            //用替换方式，因为枢轴给备份了，多出一个存储空间
            A[left]=A[right];
           while(left<right&&A[left]<=pivotKey){
               left++;
           }
           A[right]=A[left];

        }

        //把枢轴放到它真正的地方
        A[left]=pivotKey;
        return left;
    }
    //三数取中
    public int median3(int[] A,int left,int right){

        int mid=(right-left)/2;
        if(A[left]>A[right]){
            swap(A,left,right);
        }
        if(A[mid]>A[left]){
            swap(A,mid,left);
        }
        if(A[mid]>A[right]){
            swap(A,mid,right);
        }

        return A[left];
    }

    public void swap(int[] A,int i,int j){
        int temp =A[i];
        A[i]=A[j];
        A[j]=temp;
    }




【快排效率】
时间性能取决于递归的深度，可以用递归树来描述递归算法的执行情况！最优情况下，partition每次划分均匀，排序n个数值，则递归树的深度为[logn]+1,第一次partition需要对整个数组扫描一遍，做n次比较，第二次对一半扫描。所以最优时间复杂度 Ο(n log n)　，最差时间复杂度 Ο(n^2)　，平均时间复杂度Ο(n log n)　。

递归导致栈空间的使用，最好空间复杂度为Ο(log n)，最差空间复杂度Ο(n)。

（八）.桶排序算法 
【桶排序的步骤】

设置一个定量的数组当作空桶子。
寻访序列，并且把项目一个一个放到对应的桶子去。
对每个不是空的桶子进行排序。
从不是空的桶子里把项目再放回原来的序列中。
（九）.计数排序算法（实际上就是桶排序算法）

【特点】 
1. 提前必须是已知待排序的关键字为整型且范围已知。 
2. 时间复杂度为O(n+k)，n指的是桶的个数，k指的是待排序数组的长度，不是基于比较的排序算法，因此效率非常之高。 
3. 稳定性好，这个是计数排序非常重要的特性，可以用在后面介绍的基数排序中。 
4. 但需要一些辅助数组，如C[0..k]，因此待排序的关键字范围0~k不宜过大。

   
   
        import java.util.*;

        public class CountingSort {
            public int[] countingSort(int[] A, int n) {
                if(A==null ||n<2){
                    return A;
                }
                //找出桶的范围,即通过要排序的数组的最大最小值来确定桶范围
                int min=A[0];
                int max=A[0];
                for(int i=0;i<n;i++){
                    min=Math.min(A[i],min);
                    max=Math.max(A[i],max);
                }
                //确定桶数组，桶的下标即为需排序数组的值，桶的值为序排序数同一组值出现的次数
                int[] arr = new int[max-min+1];
                //往桶里分配元素
                for(int i=0;i<n;i++){
                    arr[A[i]-min]++;
                }

            //从桶中取出元素
            int index=0;
            for(int i=0;i<arr.length;i++){
                while(arr[i]-->0){
                    A[index++]=i+min;
                }
            }

            return A;
        }
    }

（十）.基数排序算法（基于桶排序）

【原理】基数排序（Radix sort）是一种非比较型整数排序算法，其原理是将整数按位数切割成不同的数字，然后按每个位数分别比较。由于整数也可以表达字符串（比如名字或日期）和特定格式的浮点数，所以基数排序也不是只能使用于整数。

将所有待比较数值（正整数）统一为同样的数位长度，数位较短的数前面补零。然后，从最低位开始，依次进行一次排序。这样从最低位排序一直到最高位排序完成以后，数列就变成一个有序序列。

【题目】对于一个int数组，请编写一个基数排序算法，对数组元素排序。 
给定一个int数组A及数组的大小n，请返回排序后的数组。保证元素均小于等于2000。

    import java.util.*;
    import java.lang.Math;
    public class RadixSort {
        public int[] radixSort(int[] A, int n) {
            //基于桶排序的基数排序

        //确定排序的趟数，即排序数组中最大值为809时，趟数为3
         int max=A[0];
        for(int i=0;i<n;i++){
            if(A[i]>max){
                max= A[i];
            }
        }
        //算出max的位数
        int time=0;
        while(max>0){
            max/=10;
            time++;
        }
        //【桶】初始化十个链表作为桶，用户分配时暂存
        ArrayList<ArrayList<Integer>> list = new ArrayList<ArrayList<Integer>>();
        for(int i=0;i<10;i++){
            ArrayList<Integer> Item = new ArrayList<Integer>();
            list.add(Item);
        }

        //进行time次分配和收集
        for(int i=0;i<time;i++){

            //分配元素，按照次序优先，从个位数开始
            for(int j=0;j<n;j++){
                int index = A[j]%(int)Math.pow(10,i+1)/(int)Math.pow(10,i);
                list.get(index).add(A[j]);
            }
            //收集元素，一个一个桶地收集
            int count=0;
            //10个桶
            for(int k=0;k<10;k++){
                //每个桶收集
                if(list.get(k).size()>0){

                    for(int a: list.get(k)){
                        A[count]=a;
                        count++;   
                    }
                  //清除数据，以便下次收集
                    list.get(k).clear();
                }
            }
        }
        return A; 
    }

【基数排序效率】
基数排序的时间复杂度是O(k·n)，其中n是排序元素个数，k是数字位数。注意这不是说这个时间复杂度一定优于O(n·log(n))，k的大小取决于数字位的选择和待排序数据所属数据类型的全集的大小；k决定了进行多少轮处理，而n是每轮处理的操作数目。

基数排序基本操作的代价较小，k一般不大于logn，所以基数排序一般要快过基于比较的排序，比如快速排序。

最差空间复杂度是O(k·n)

