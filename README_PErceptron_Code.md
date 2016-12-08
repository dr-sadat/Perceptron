function  customPerceptron(x,w,i)
idx = x(:,4);
noerrcnt = 0;
wx = 0;
i1 = 1;
iter = 1;
while(iter <= 1000)
noerrcnt = 0;
for i = 1:length(x)
    wx = 0;
    for j = 1:3
        wx = wx + (w(i1,j) * x(i,j));  
    end
    if(wx == 0)
        if(x(i,4) == 1)
           w((i1 + 1),:) = w(i1,:) - x(i,1:3);
        else
           w((i1 + 1),:) = w(i1,:) + x(i,1:3);
        end
    elseif(wx < 0)
        if(x(i,4) == 2)
           w((i1 + 1),:) = w(i1,:) + x(i,1:3);
        else
           w((i1 + 1),:) = w(i1,:);
           noerrcnt = noerrcnt + 1;
        end
    else    
        if(x(i,4) == 1)
           w((i1 + 1),:) = w(i1,:) - x(i,1:3);
        else
           w((i1 + 1),:) = w(i1,:);
           noerrcnt = noerrcnt + 1;
        end  
    end
    i1 = i1 + 1;
end 
iter = iter + 1;
end

%% Equation
l = length(w);
a = (w(l,1) * -1)/w(l,2);
b = (-1 * w(l,3))/w(l,2);
out = (a * x(:,1))+ b;
figure()
hold on
plot(x(idx==1,1),x(idx==1,2),'c.','MarkerSize', 15);
plot(x(idx==2,1),x(idx==2,2),'b*','MarkerSize', 15);
plot(x(:,1),out,'-');
if w(1,2) ~= 0
c = (w(1,1) * -1)/w(1,2);
d = (-1 * w(1,3))/w(1,2);
else
c = 0;d =0;   
end    
iw = (c * x(:,1))+ d;
plot(x(:,1),iw,'--r');
hold off
end
