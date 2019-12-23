使用cyclone IV E系列来初学入门

代码如下

```verilog
module float_water_led(

​                   input clk,                       //输入端口定义

​                    output reg [7:0] led = 8'b00000001   //输出端口定义

​                   );

  reg [24:0] counter = 25'd0;       //计数值

  reg [7:0] tmp=8'b1;       //加入一个标志符，方便进行移位

  always @ (posedge clk)    /循环块

   begin

​     if (counter==25'd24999999)     //分频，1HZ

​     begin

​       led<=~tmp;     //led低电平有效

​       tmp<=tmp>>1;  //使标识符取反

​    end

   else

​     counter<=counter+1;    //计数值加一

  end

endmodule


```





  不同的开发板所用代码不一定相同，请谨慎复制