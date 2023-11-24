# 用 C 语言实现最小二乘法算法

有些嵌入式系统的 IDE 不支持结构体，所以改了一个通俗易懂版本。

```
#include <stdio.h>
#define LEN 100
float DataInX[LEN];
float DataInY[LEN];
unsigned char GucDataLength;
void push(float x, float y)
{
  int i = 0;
  if (GucDataLength < LEN)
  {
    DataInX[GucDataLength] = x;
    DataInY[GucDataLength++] = y;
    return;
  }
  //数据移动,去掉最后一个数据
  for (i = 0; i < LEN - 1; i++)
  {
    DataInX[i] = DataInX[i + 1];
    DataInY[i] = DataInY[i + 1];
  }
  DataInY[LEN] = x;
  DataInY[LEN] = y;
  GucDataLength = LEN;
}
float calc(float x)
{
  int i = 0;
  float mean_x = 0;
  float mean_y = 0;
  float num1 = 0;
  float num2 = 0;
  float a = 0;
  float b = 0;
  //求t,y的均值
  for (i = 0; i < GucDataLength; i++)
  {
    mean_x += DataInX[i];
    mean_y += DataInY[i];
  }
  mean_x /= GucDataLength;
  mean_y /= GucDataLength;
  printf("mean_x = %f,mean_y = %f\n", mean_x, mean_y);
  for (i = 0; i < GucDataLength; i++)
  {
    num1 += (DataInX[i] - mean_x) * (DataInY[i] - mean_y);
    num2 += (DataInX[i] - mean_x) * (DataInX[i] - mean_x);
  }
  a = num1 / num2;
  b = mean_y - b * mean_x;
  printf("a = %f,b = %f\n", a, b);
  return (a * x + b);
}
int main()
{
  float data_x[7] = {0, 1, 2, 3, 4, 5, 6};
  float data_y[7] = {-88, 16, -20, 11, 1, 1, -60};
  int i = 0;
  for (i = 0; i < 7; i++)
  {
    push(data_x[i], data_y[i]);
  }
  /* 计算x=10时y值 */
  printf("data_y[10] = %f\n", calc(10));
  return 0;
}
```

转载：[用C语言实现最小二乘法算法](https://blog.51cto.com/u_15077560/4686280)
