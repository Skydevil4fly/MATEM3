# MATEM3
MATLAB TEMP FILE

```plaintext
1A.

>> A=[4 6 9;3 0 9;5 3 15];
>> det(A)
ans =
 -27.0000
>> transpose(A)
ans =
 4 3 5
 6 0 3
 9 9 15
>> rank(A)
ans =
 3

1b) 

s=0;
n=10;
for i=1:n
 s=s+(1/(i^2+1));
end
fprintf('Sum of the series is %f\n',s)
>> testeq
Sum of the series is 0.981793
 
OR

>> syms t w
>> f=cos(3*t)+sin(2*t);
>> fourier(f,t,w)
ans =
pi*(dirac(w - 3) + dirac(w + 3)) - pi*(dirac(w - 2) - dirac(w + 2))*i

2 a)
x = linspace(0,3);
y = x.^2+x+2;
ry = repmat(y,1,3);
rx = linspace(0,9,length(ry));
plot(rx,ry,'k*')
xlabel('x')
ylabel('f(x)')
grid on

OR

f= @(x) (x).*(0<=x & x<pi)+(2*pi-x).*(pi<=x & x<2*pi);
x1=linspace(0,2*pi,1000);
pfx = repmat(f(x1),1,4);
x2 = linspace(-4*pi,4*pi,length(pfx));
plot(x2,pfx,'*b')
grid

2b) 
x=linspace(-2,2,5);
y=linspace(-2,2,5);
z=linspace(-2,2,5);
[x,y,z]=meshgrid(x,y,z);
f1=x;
f2=y.^2;
f3=z.^2+1;
quiver3(x,y,z,f1,f2,f3)
xlabel('x')
ylabel('y')
zlabel('z')


3.

function [poly] = lag_poly(x,y)
n=length(x);
syms t
poly=0;
for i=1:n
 L=1;
 for j=1:n
 if(i~=j)
 L=L*(t-x(j))/(x(i)-x(j));
 end
 end
 poly=poly+L*y(i);
end
poly=simplify(poly);
t = x(1):0.001:max(x);
z = eval(poly);
plot(x,y,'*k',t,z,'k')
legend('Data Points','Lagrange Polynomial')
end

>> x=[5 6 9 11];y=[12 13 14 16];
>> [poly] = lag_poly(x,y)

poly =
t^3/20 - (7*t^2)/6 + (557*t)/60 - 23/2
𝑓(10) = 14.6667


4. Trapezoidal rule

function [I] = trapez(f,a,b,n) 
h=(b-a)/n;
x=a:h:b; 
I= (h/2)*(f(a)+2*sum(f(x(2:n)))+f(b));
end

>> f=@(x) 1./(1+x.^2);
>> a=0; b=6; n=6;
>> trapez(f,a,b,n) 
ans = 1.4108
 
OR

4. Simpson’s 1/3rd rule

function [I] = simpson13(f,a,b,n)
h=(b-a)/n;
x=a:h:b;
I= (h/3)*(f(a)+4*sum(f(x(2:2:n)))+2*sum(f(x(3:2:n-1)))+f(b));
end

>> f=@(x) 1./(1+x.^2);
>> a=0; b=6; n=6;
>> simpson13(f,a,b,n)
ans = 1.3662

