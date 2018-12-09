# Задание 59
Дан массив A[n;n]  Расположить элементы массива по возрастанию, двигаясь по спирали по часовой стрелке, начиная от центра.
>Delphi

```dpr
program LR6;

{$APPTYPE CONSOLE}

uses
  SysUtils;

const   N=4;
   Type TMas=array[1..N,1..N] of integer;

 procedure RandomArr(var A:Tmas);
  var i,j:integer;
   begin
      Randomize;
     for i:=1 to N do
      for j:=1 to N do
      A[i,j] := Random(100)-50;

   end;

  procedure SetArr(var A:Tmas);
   var i,j,k:Integer;
    begin
       k:=1;
       for i:=1 to N do
       for j:=1 to N do
      begin
       A[i,j] := k;
       k:=k+1;
      end;
    end;

 procedure IntArr(var A:Tmas);
  var i,j:integer;
   begin
    for i:=1 to N do
    for j:=1 to N do
    readln(A[i,j]);
   end;

    procedure Swap( var A,B: integer);
 var temp:Integer;
    begin
      temp:=A;
      A:=B;
      B:=temp;
    end;


 procedure Direction( var k,i,j:Integer);
  begin
      case k mod 4 of
        0:begin
          inc(j);{right}
          if j=N-i+2 then inc (k);
          end;

        1:begin
          inc(i);{down}
          if j=i then inc(k);
          end;

        2:begin
           dec(j);{left}
           if j=N-i+1 then inc(k);
          end;

        3:begin
           dec(i);{up}
           if j=i then inc(k);
          end;
      end;
  end;

 procedure Next( num:integer; var i,j,k:integer) ;
 var z:Integer;
 begin
   i:=N div 2+1;
   j:=N div 2+1;
      if N mod 2=0
       then k:=2
       else k:=0;
   for z:=1 to num-1 do
    Direction(k,i,j);
 end;

  procedure Sort(  var A:TMas;  var i,j,k:integer; num:Integer) ;
 var z,i_min,j_min,i_beg,j_beg,min:Integer;

 begin
   min:=A[i,j];
   i_beg:=i;
   j_beg:=j;
   i_min:=i;
   j_min:=j;
   for z:=num to N*N-1 do
    begin
      Direction(k,i,j);
      if  A[i,j] < min then
      begin
       min:=A[i,j];
       i_min:=i;
       j_min:=j;
      end;

    end;
   Swap(A[i_beg,j_beg],A[i_min,j_min]);
 end;

 procedure Output (A:Tmas);
  var i,j:Integer;
   begin
     for i:=1 to N do
     begin
      for j:=1 to N do
      write(A[i,j]:5);
      Writeln;
     end;
   end;



var Arr:TMas;
    number,i,j,k:integer;

  BEGIN
    RandomArr(Arr);
   //SetArr(Arr);
   //IntArr(Arr);
    Output(Arr);
    Writeln ('');
        for number:=1 to N*N-1 do
          begin
           Next(number,i,j,k);
           Sort(Arr,i,j,k,number);
          end;

   Output(Arr);
   Readln;
  END.
  ```
