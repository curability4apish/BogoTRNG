#include<stdio.h>
#include<windows.h>
#include<math.h>

int samp(double x)
{
    if (x<0) x*=-1;
    x-=(int) x;
    x*=10000;
    x=(int)x%16;
    if (x<10) return (x+48);
    else return (x+87);
}
int reverse(int num)
{
    int reversed = 0;
    if (num%10==0) num+=1;
    while(num != 0)
    {
        reversed = reversed * 10 + num % 10;
        num = num / 10;
    }
    return reversed;
}
/* reverse 數字反轉函數
用法舉例：
reverse(1234567)=7654321
然而
reverse(4567890)=reverse(4567890+1)=1987654
是為了避免反轉位數的消減與熵減
*/
int main()
{
    for (int i=0;i<64;i++){
    int a[2]={0}; // 儲存兩筆運行時間
    double aa=0;
    // 兩筆運行時間經過增熵處理後的隨機變數
    int loop=0; // 共執行兩次Bogo排序
    // 第一次在loop=0, 第二次在loop=1.

    LARGE_INTEGER start, end;// 宣告開始與結束的時間戳記
    long long tick_taken; // 宣告運行時間 (單位：tick)
    /*
    1 tick=100奈秒
    因為透過以下指令:
    QueryPerformanceFrequency(&frequency); printf("%d",frequency);
    可得 frequency=10000000
    */
    start:

    QueryPerformanceCounter(&start); //紀錄開始時間
    srand(1000);//設定rand()產生器的初始值

    int random=0,temp=0;
    int input[]={68,14,78,98,67,89,45,90,87};
    redo:// Shuffle data
    for (int i=0;i<10;i++)
    {
        random=rand()%10;
        temp=input[random];
        input[random]=input[i];
        input[i]=temp;
        // 序列洗牌：對於每一個數做隨機的交換位置
    }
    for (int i=0;i<9;i++)
    {
        if (input[i]>input[i+1]) goto redo;
    } // 檢查序列是否已經排序成功，若否則回到redo重新洗牌
    QueryPerformanceCounter(&end); // 紀錄結束時間
    tick_taken = (end.QuadPart - start.QuadPart);
    // 單次排序所消耗的時間(單位：tick)
    //printf("Tick taken: %d\n", tick_taken);
    a[loop]=tick_taken;// 儲存單次排序所消耗的時間
    loop++; if (loop==1) goto start;// 完成第一輪排序後進行下一輪

    a[0]=reverse(a[0]); // 反轉增熵
    a[1]=reverse(a[1]); // 反轉增熵
    aa=a[0]*(cos(a[1]*M_PI))-a[1]*(sin(a[0]*M_E));
    if (aa<0) aa*=-1;
    while (aa<100) aa*=M_E;
    while (aa>1000) aa/=M_PI;
    // 增熵處理與值域控制
    //printf("%d",(int)(aa*10)%2);
    printf("%c",(char)samp(aa));
    }
    return 0;
}
