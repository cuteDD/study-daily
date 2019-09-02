###冒泡   
O(n²)     口诀：
    外层循环 0到n-1      //控制比较轮数   n 表示元素的个数
     内层循环 0到n-i-1     //控制每一轮比较次数
     两两比较做交换

'''
public static void sort(int[] arr){
    for (int i = 1; i <arr.length ; i++) {
        for (int j = 0; j < arr.length-i; j++) {
            if (arr[j]>arr[j+1]){
                int temp=arr[j+1];
                arr[j+1] = arr[j];
                arr[j] = temp;
            }
        }
    }
 '''

 
插入排序（打扑克，第一次最前面的牌当作有序的，然后他后面的第一颗牌和他对比，如果后面小于前面就交换，反之不变，下标后移重复）
先看最好的情况，序列已经是升序的，在这种情况下，需要进行的比较操作为n-1次；最坏的情况，序列为降序序列，那此时需要进行的比较次数为n（n-1）/2次。因此，平均来说，插入排序算法时间复杂度为O（n^2）,因而，插入排序不适合数据量比较大的排序应用。
public  static void insertSort(int[] arr) {
    if (arr.length < 2) {
        return;
    }
    for (int i = 1; i < arr.length; i++){
        for (int j = i - 1; j >= 0 && arr[j] >= arr[j + 1]; j--) {
            swap(arr, j, j + 1);
        }
    }
}

希尔排序 O(n^（1.3—2）)
private static void shellSort(int[] source) {
    int j;
    for (int gap = source.length / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < source.length; i++) {
            int temp = source[i];
            for (j = i; j >= gap && temp < source[j - gap]; j -= gap)
                source[j] = source[j - gap];
            source[j] = temp;
        }
    }
}

快排  O (nlogn)
public static void quickSort(int[] arr, int low, int high) {
    int i, j, temp, t;
    if (low > high) {
        return;
    }
    i = low;
    j = high;
    //temp就是基准位
    temp = arr[low];
    while (i < j) {
        //先看右边，依次往左递减
        while (temp <= arr[j] && i < j) {
            j--;
        }
        //再看左边，依次往右递增
        while (temp >= arr[i] && i < j) {
            i++;
        }
        //如果满足条件则交换
        if (i < j) {
            t = arr[j];
            arr[j] = arr[i];
            arr[i] = t;
        }
    }
    //最后将基准为与i和j相等位置的数字交换
    arr[low] = arr[i];
    arr[i] = temp;
    //递归调用左半数组
    quickSort(arr, low, j - 1);
    //递归调用右半数组
    quickSort(arr, j + 1, high);
}








平方根
public class Lesson3_2 {
 
 /**
    * @Description: 计算大于 1 的正整数之平方根
    * @param n- 待求的数, deltaThreshold- 误差的阈值, maxTry- 二分查找的最大次数
    * @return double- 平方根的解
    */
    public static double getSqureRoot(int n, double deltaThreshold, int maxTry) {
     
     if (n <= 1) {
      return -1.0;
     }
     
     double min = 1.0, max = (double)n;
     for (int i = 0; i < maxTry; i++) {
      double middle = (min + max) / 2;
      double square = middle * middle;
      double delta = Math.abs((square / n) - 1);
      if (delta <= deltaThreshold) {
       return middle;
      } else {
       if (square > n) {
        max = middle;
       } else {
        min = middle;
       }
      }
     }
     return
    }
}
public static void main(String[] args) {
  int number = 10;
  double squareRoot = Lesson3_2.getSqureRoot(number, 0.000001, 10000);
  if (squareRoot == -1.0) {
   System.out.println(" 请输入大于 1 的整数 ");
  } else if (squareRoot == -2.0) {
   System.out.println(" 未能找到解 ");
  } else {
   System.out.println(String.format("%d 的平方根是 %f", number, squareRoot));
  }  
 }

二分查找
public class Demo3 {
    public static void main(String[] args) { 
        int[] arr = {2,4,6,7,43,57,90,101};
        int number = 10;
        System.out.println(method(arr, number));
    }
    
    public static int method(int[] arr,int number){
        int start = 0; //定义变量，记录最小的索引
        int end = arr.length-1; //定义变量，记录最大的索引
        int mid = (start+end)/2; //定义变量，记录中间的索引 
        while(arr[mid]!=number) {  //只要查找的数不等于数组中间的数，就继续查找，如果中间的数等于查找的数，则mid就是要求的索引
         if(number<arr[mid]) {  //如果这个数比数组中间的数小，则让最大的索引=mid-1
                end = mid-1;
      }else if(number>arr[mid]) {  //如果这个数比数组中间的数大，则让最小的所用=mid+1
                start = mid+1;
            }
            if(start>end) {    //如果出现最小索引大于最大索引的情况，说明数组中不存在这样的元素
                return -1;
            }
            mid = (start+end)/2;  //每次循环后，因为首尾的索引变化了，所以中间的索引也需要变化
        }
        return mid;  //如果数组中有这个元素，则返回
    }
    

}