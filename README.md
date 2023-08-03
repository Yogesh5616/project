# project
#matlab codes for solving different differential equation
clear
clearvars

dt=0.001;
tend= 1;
dx=0.01;
xend=1;
dy = 0.01;
yend = 1;

t=0:dt:tend;
x = 0:dx:xend;
y = 0:dy:yend;
Nt = numel(t);
Nx = numel(x);
Ny = Nx;
u = zeros(Nx,Ny,Nt);
A = dt^2/dx^2;
B = dt^2/dy^2;

%initial condition
u(:,:,1)=1;
u(:,:,2)=u(:,:,1);
err = 1;
iter = 1;
while err >1e-6 && iter <1000

 

for k = 2:Nt
    for i = 2:Nx-1
        for j = 2:Ny-1
        u(i,j,k+1) = u(i,j,k-1)+u(i,j,k) - dt*(u(i,j,k)-u(i,j,k-1)) + A*(u(i+1,j,k)-2*u(i,j,k)+u(i-1,j,k)) + B*(u(i,j+1,k)-2*u(i,j,k)+u(i,j-1,k)) - (dt^2/u(i,j,k)); 
        end
    end
        u(1, :, :) = 1;                
        u(end, :, :) = 1;              
        u(:, 1, :) = 1;                 
        u(:, end, :) = 1;

end
end
plot(y,x,u(:,1:100:end));
%plot(t,u);
