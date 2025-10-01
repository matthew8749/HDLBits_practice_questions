# S03-2 Sequential Logic 紀錄

# <font color=blue>**S03. Circuits**</font>

## <font color=#FF00FF>S03-1 Combinational Logic</font>

### <font color=#00C957>S03-1-1 Basic Gates</font>

### <font color=#00C957>S03-1-2 Multiplexers</font>

### <font color=#00C957>S03-1-3 Arithmetic Circuits</font>

### <font color=#00C957>S03-1-4 Karnaugh Map to Circuit</font>

##  <font color=#FF00FF>S03-2 Sequential Logic</font>

### <font color=#00C957>S03-2-1 Latches and Flip-Flops</font>

#### S03-2-1.1 D filp-flop

想法：


```verilog
module top_module (
    input clk,    // Clocks are used in sequential circuits
    input d,
    output reg q );

    always @(posedge clk ) begin
    	q <= d;
    end

endmodule
```

#### S03-2-1.2 D filp-flops

想法：

```verilog
	module top_module (
	    input clk,
	    input [7:0] d,
	    output [7:0] q
	  );
	    always @(posedge clk ) begin
	    	q <= d;
	    end

	endmodule

```

#### S03-2-1.3 DFF with reset
- Create 8 D flip-flops with active high synchronous reset
想法：


```verilog
	module top_module (
	    input clk,
	    input reset,            // Synchronous reset
	    input [7:0] d,
	    output [7:0] q
	);
	  always @(posedge clk ) begin
	      if (reset) begin
	  		q <= 7'b0;
	  	end else begin
	  		q <= d;

	  	end
	  end
	endmodule

```

#### S03-2-1.4 DFF with reset value
- Create 8 D flip-flops with active high synchronous reset. The flip-flops must be reset to 0x34 rather than zero.All DFFs should be triggered by the negative edge of clk.

想法：

```verilog
module top_module (
    input clk,
    input reset,
    input [7:0] d,
    output [7:0] q
);
  always @(negedge clk ) begin
      if (reset) begin
  		q <= 7'h34;
  	end else begin
  		q <= d;

  	end
  end
endmodule
```

#### S03-2-1.5 DFF with asynchronous reset  
- Create 8 D flip-flops with active high asynchronous reset. All DFFs should be triggered by the positive edge of clk.  

想法：
	注意是"active high asynchronous reset"

```verilog
module top_module (
  input clk,
  input areset,   // active high asynchronous reset
  input [7:0] d,
  output [7:0] q
);
always @(posedge clk or posedge areset) begin
	if ( areset ) begin
		 q <= 7'b00;
	end else begin
		 q <= d;
	end
end

endmodule

```

#### S03-2-1.6 DFF with byte enable  
- Create 16 D flip-flops. It's sometimes useful to only modify parts of a group of flip-flops. The byte-enable inputs control whether each byte of the 16 registers should be written to on that cycle. byteena[1] controls the upper byte d[15:8], while byteena[0] controls the lower byte d[7:0].  

	resetn is a synchronous, active-low reset.  

	All DFFs should be triggered by the positive edge of clk.  

想法：

```verilog
module top_module (
    input clk,
    input resetn,
    input [1:0] byteena,
    input [15:0] d,
    output [15:0] q
);
  always @ (posedge clk) begin
  	if (!resetn) begin
  		q <= 15'b0;
  	end else begin
  		q[7: 0] <= (byteena[0]) ? d[7: 0] : q[7: 0];
  		q[15: 8] <= (byteena[1]) ? d[15: 8] : q[15: 8];
  	end
  end

endmodule

```



#### S03-2-1.7 D Latch  

想法 :   

```verilog

```
#### S03-2-1.8 DFF  

想法 :   

```verilog

```
#### S03-2-1.9 DFF  

想法 :   

```verilog

```
#### S03-2-1.10 DFF+gate  

想法 :   

```verilog

```
#### S03-2-1.11 Mux and DFF

想法 :   
題目要求的只是包含DFF和MUX的submodule  
submodule的名稱就叫top_module(題目要求)  

```verilog


```

#### S03-2-1.12 Mux and DFF

想法 :   
判斷的優先順序，E 先

等等!先判斷L好像比較好理解

```verilog


```

#### S03-2-1.13 DFFs and gates

想法 :   
分別做 xor、 and、 or ，在做nor
```verilog


```

#### S03-2-1.14 Create circuit from truth table

想法 :   
```verilog


```

#### S03-2-1.15 Detect an edge

想法 :   
```verilog


```

#### S03-2-1.16 Detect both edges

想法 :   
正緣檢測公式加(邏輯或)負緣檢測公式
正緣檢測公式 : ~in_d1 & in
負緣檢測公式 : in_d1 & ~in
```verilog


```

#### S03-2-1.17 Edge capture register

想法 :   
```verilog


```

#### S03-2-1.18 Dual-edge triggered flip-flop

想法 :   
```verilog


```


### <font color=#00C957>S03-2-2 Counters</font>
### <font color=#00C957>S03-2-3 Shift Registers</font>
### <font color=#00C957>S03-2-4 More Circuits</font>

---  

### <font color=#00C957>S03-2-5 Finite State Machines</font>

#### S03-2-5.1 Simple FSM 1 (asynchronous reset)  
想法：  
把`S03-2-5.1`的程式碼改成sync 

```verilog

```

#### S03-2-5.2 Simple FSM 1 (synchronous reset)  
想法：  


```verilog

```

#### S03-2-5.3 Simple FSM 2 (asynchronous reset)  
想法：  


```verilog

```

#### S03-2-5.4 Simple FSM 2 (synchronous reset)  
想法：  


```verilog

```

#### S03-2-5.5 Simple state transitions 3  
想法：  


```verilog

```

#### S03-2-5.6 Simple one-hot state transitions 3  
想法：  


```verilog

```

#### S03-2-5.7 Simple FSM 3 (asynchronous reset)  
想法：  


```verilog

```

#### S03-2-5.8 Simple FSM 3 (synchronous reset)  
想法：  


```verilog

```

#### S03-2-5.9 Design a Moore FSM  
想法：  
首先要理解題目
s1, s2, s3 是傳感器，當水位到達此高度傳感器便會輸出1



```verilog

```

#### S03-2-5.10 Lemmings 1  
想法：  


```verilog

```

#### S03-2-5.11 Lemmings 2  
想法：  


```verilog

```

#### S03-2-5.12 Lemmings 3  
想法：  


```verilog

```

#### S03-2-5.13 Lemmings 4  
想法：  


```verilog

```

#### S03-2-5.14 One-hot FSM  
想法：  


```verilog

```

#### S03-2-5.15 PS/2 packet parser  
想法：  


```verilog

```

#### S03-2-5.16 PS/2 packet parser and datapath  
想法：  


```verilog

```

#### S03-2-5.17 Serial receiver  
想法：  


```verilog

```

#### S03-2-5.18 Serial receiver and datapath  
想法：  


```verilog

```

#### S03-2-5.19 Serial receiver with parity checking  
想法：  


```verilog

```

#### S03-2-5.20 Sequence recognition  
想法：  


```verilog

```

#### S03-2-5.21 Q8: Design a Mealy FSM  
想法：  


```verilog

```

#### S03-2-5.22 Q5a: Serial two's complementer (Moore FSM)  
想法：  


```verilog

```

#### S03-2-5.23 Q5b: Serial two's complementer (Mealy FSM)  
想法：  


```verilog

```

#### S03-2-5.24 Q3a: FSM  
想法：  


```verilog

```

#### S03-2-5.25 Q3b: FSM  
想法：  


```verilog

```

#### S03-2-5.26 Q3c: FSM logic  
想法：  


```verilog

```

#### S03-2-5.27 Q6b: FSM next-state logic  
想法：  


```verilog

```

#### S03-2-5.28 Q6c: FSM one-hot next-state logic  
想法：  


```verilog

```

#### S03-2-5.29 Q6: FSM  
想法：  


```verilog

```

#### S03-2-5.30 Q2a: FSM  
想法：  


```verilog

```

#### S03-2-5.31 Q2b: One-hot FSM equations  
想法：  


```verilog

```

#### S03-2-5.32 Q2a: FSM  
想法：  


```verilog

```

#### S03-2-5.33 Q2b: Another FSM  
想法：  


```verilog

```


## <font color=#FF00FF>S03-3 Building Larger Circuits</font>