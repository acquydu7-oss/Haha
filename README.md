local pl=game:GetService("Players").LocalPlayer
local pg=pl:WaitForChild("PlayerGui")
local U=game:GetService("UserInputService")
local T=game:GetService("TweenService")
local R=game:GetService("RunService")
local V=Vector3.new
local C=Color3.fromRGB
local o=pg:FindFirstChild("HTT")if o then o:Destroy()end
local g=Instance.new("ScreenGui",pg)
g.Name="HTT"g.ResetOnSpawn=false g.IgnoreGuiInset=true g.DisplayOrder=999
local m=Instance.new("Frame",g)
m.Size=UDim2.new(0,190,0,160)m.Position=UDim2.new(0,20,0,100)
m.BackgroundColor3=C(18,5,30)m.BorderSizePixel=0
Instance.new("UICorner",m).CornerRadius=UDim.new(0,12)
local h=Instance.new("TextLabel",m)
h.Size=UDim2.new(1,0,0,32)h.BackgroundColor3=C(80,25,120)
h.Text="  HOLLOW PURPLE"h.TextColor3=C(230,180,255)
h.TextSize=15 h.TextXAlignment=Enum.TextXAlignment.Left
h.Font=Enum.Font.GothamBold
local bc=Instance.new("Frame",m)
bc.Size=UDim2.new(1,-10,1,-40)bc.Position=UDim2.new(0,5,0,38)
bc.BackgroundTransparency=1
Instance.new("UIListLayout",bc).Padding=UDim.new(0,4)
local function B(t,c)local b=Instance.new("TextButton",bc)
b.Size=UDim2.new(1,0,0,26)b.BackgroundColor3=c b.Text=t
b.TextColor3=C(255,255,255)b.TextSize=12 b.Font=Enum.Font.GothamBold
Instance.new("UICorner",b).CornerRadius=UDim.new(0,6)return b end
local bC=B("CAST PURPLE",C(120,30,180))
local bS=B("BLUE SPEAR",C(20,60,150))
local bA=B("AUTO: OFF",C(60,60,60))
local dg=false dS,sP
h.InputBegan:Connect(function(i)if i.UserInputType==Enum.UserInputType.MouseButton1 then dg=true dS=i.Position sP=m.Position end end)
h.InputEnded:Connect(function(i)if i.UserInputType==Enum.UserInputType.MouseButton1 then dg=false end end)
U.InputChanged:Connect(function(i)if dg and i.UserInputType==Enum.UserInputType.MouseMovement then
local d=i.Position-dS m.Position=UDim2.new(sP.X.Scale,sP.X.Offset+d.X,sP.Y.Scale,sP.Y.Offset+d.Y)end end)
print("[HTT] Menu OK")
local ch,ro,cast,pose,auto=false,false,false
local sAct=false
local ef,oC0={},{}
local sCn
local function shk(d,mag)
if sCn then sCn:Disconnect()end
local c=workspace.CurrentCamera if not c then return end
local t=0
sCn=R.RenderStepped:Connect(function(dt)
if t>=d then sCn:Disconnect()sCn=nil return end
t=t+dt local f=1-t/d
c.CFrame=c.CFrame*CFrame.new((math.random()-.5)*mag*f,(math.random()-.5)*mag*f,(math.random()-.5)*mag*f)end)end
local function TJ(mo,c,t)if mo and mo.Parent then
T:Create(mo,TweenInfo.new(t),{C0=c}):Play()end end
local function kk()
if pose then return end pose=true oC0={}
for _,d in ipairs(ch:GetDescendants())do if d:IsA("Motor6D")then oC0[d]=d.C0 end end
if ch:FindFirstChild("UpperTorso")then
TJ(ch.RightUpperArm:FindFirstChild("RightShoulder"),CFrame.new(1,.5,0)*CFrame.Angles(math.rad(-75),math.rad(-15),math.rad(-55)),.5)
TJ(ch.LeftUpperArm:FindFirstChild("LeftShoulder"),CFrame.new(-1,.5,0)*CFrame.Angles(math.rad(-75),math.rad(15),math.rad(55)),.5)
TJ(ch.RightLowerArm:FindFirstChild("RightElbow"),CFrame.new(0,1,0)*CFrame.Angles(0,math.rad(-30),math.rad(-95)),.5)
TJ(ch.LeftLowerArm:FindFirstChild("LeftElbow"),CFrame.new(0,1,0)*CFrame.Angles(0,math.rad(30),math.rad(95)),.5)
TJ(ch.RightHand:FindFirstChild("RightWrist"),CFrame.new(0,.5,0)*CFrame.Angles(math.rad(-30),0,math.rad(-20)),.5)
TJ(ch.LeftHand:FindFirstChild("LeftWrist"),CFrame.new(0,.5,0)*CFrame.Angles(math.rad(-30),0,math.rad(20)),.5)
else local ut=ch:FindFirstChild("Torso")if ut then
TJ(ut:FindFirstChild("Right Shoulder"),CFrame.new(1,.5,0)*CFrame.Angles(math.rad(-75),math.rad(-15),math.rad(-55)),.5)
TJ(ut:FindFirstChild("Left Shoulder"),CFrame.new(-1,.5,0)*CFrame.Angles(math.rad(-75),math.rad(15),math.rad(55)),.5)end end
local nk=ch.Head:FindFirstChild("Neck")
if nk and oC0[nk]then TJ(nk,oC0[nk]*CFrame.Angles(math.rad(-8),0,0),.5)end end
local function rk()
if not pose then return end pose=false
for mo,c in pairs(oC0)do if mo and mo.Parent then
T:Create(mo,TweenInfo.new(.4),{C0=c}):Play()end end end
local function orb(p,c,s)
local o=Instance.new("Part",workspace)
o.Shape=Enum.PartType.Ball o.Size=V(s,s,s)o.Position=p
o.Anchored=true o.CanCollide=false o.Material=Enum.Material.Neon
o.Color=c
local l=Instance.new("PointLight",o)l.Color=c
ef[#ef+1]=o return o end
local function rng(p,c,s)
local r=Instance.new("Part",workspace)
r.Shape=Enum.PartType.Cylinder r.Size=V(.3,s,s)
r.Anchored=true r.CanCollide=false r.Material=Enum.Material.Neon
r.Color=c r.Transparency=.3
r.CFrame=CFrame.new(p)*CFrame.Angles(0,0,math.rad(90))
ef[#ef+1]=r return r end
local function bolt(a,b,th)
task.spawn(function()
local pv=a
for i=1,8 do
if not ch or not ch.Parent then break end
local s=a+(b-a)*(i/8)+V(math.random(-3,3),math.random(-3,3),math.random(-3,3))
local p=Instance.new("Part",workspace)
p.Size=V(th,th,(s-pv).Magnitude)p.CFrame=CFrame.new((pv+s)/2,s)
p.Anchored=true p.CanCollide=false p.Material=Enum.Material.Neon
p.Color=C(30,0,50)
local l=Instance.new("PointLight",p)l.Color=C(80,0,150)l.Brightness=6 l.Range=20
ef[#ef+1]=p
task.delay(.25,function()if p.Parent then p:Destroy()end end)
pv=s task.wait(.015)end end)end
local function stm(c,dur)
task.spawn(function()
local t=0
while t<dur do
if not ch or not ch.Parent then break end
task.spawn(function()
local a=math.random()*math.pi*2 d=math.random(10,60)
bolt(c+V(math.cos(a)*d,120,math.sin(a)*d),c+V(math.cos(a)*d,0,math.sin(a)*d),math.random(8,18)/10)end)
t=t+.12 task.wait(.12)end end)end
local function spr(op,dir)
task.spawn(function()
local s=Instance.new("Part",workspace)
s.Shape=Enum.PartType.Cylinder s.Size=V(18,.6,.6)
s.Material=Enum.Material.Neon s.Color=C(255,20,40)
s.Anchored=true s.CanCollide=false s.Transparency=.05
s.CFrame=CFrame.new(op,op+dir)*CFrame.Angles(0,math.rad(90),0)
local l=Instance.new("PointLight",s)l.Color=C(255,40,40)l.Brightness=8 l.Range=25
ef[#ef+1]=s
local tg=op+dir*200
T:Create(s,TweenInfo.new(.9),{CFrame=CFrame.new(tg,tg+dir)*CFrame.Angles(0,math.rad(90),0),Transparency=1}):Play()
task.delay(1,function()if s.Parent then s:Destroy()end end)end)end
local rp=RaycastParams.new()
rp.FilterType=Enum.RaycastFilterType.Exclude
local function drt(c,n)
task.spawn(function()
rp.FilterDescendantsInstances={ch}
for i=1,n do
if not ch or not ch.Parent then break end
task.spawn(function()
local a=math.random()*math.pi*2 d=math.random(5,60)
local x=c.X+math.cos(a)*d z=c.Z+math.sin(a)*d
local r=workspace:Raycast(V(x,c.Y+5,z),V(0,-100,0),rp)
local gy=r and r.Position.Y or c.Y-3
local b=Instance.new("Part",workspace)
b.Size=V(math.random(10,35)/10,math.random(10,30)/10,math.random(10,35)/10)
b.Position=V(x,gy+.5,z)b.Anchored=false b.CanCollide=true
b.Material=Enum.Material.Slate
local sh=math.random()
b.Color=sh<.4 and C(90,60,40)or(sh<.7 and C(70,50,35)or C(110,80,55))
b.CFrame=CFrame.new(b.Position)*CFrame.Angles(math.random()*math.pi*2,math.random()*math.pi*2,math.random()*math.pi*2)
b.Velocity=V(math.random(-60,60),math.random(80,180),math.random(-60,60))
b.RotVelocity=V(math.random(-30,30),math.random(-30,30),math.random(-30,30))
ef[#ef+1]=b
task.delay(4,function()if b.Parent then b:Destroy()end end)end)
task.wait(.02)end end)end
local function drtC(c,dur,rate)
task.spawn(function()
local t=0
while t<dur do
if not ch or not ch.Parent then break end
drt(c,3)t=t+rate task.wait(rate)end end)end
local function pul(o)
task.spawn(function()
for i=1,25 do
if not o or not o.Parent then break end
task.spawn(function()
local a=math.random()*math.pi*2 d=math.random(20,55)sz=math.random(2,6)
local p=Instance.new("Part",workspace)
p.Size=V(sz,sz,sz)p.Anchored=true p.CanCollide=false
p.Material=Enum.Material.Neon
p.Color=C(math.random(120,180),math.random(180,240),255)
p.Transparency=.2
p.Position=o.Position+V(math.cos(a)*d,math.random(-15,15),math.sin(a)*d)
ef[#ef+1]=p
T:Create(p,TweenInfo.new(.8),{Position=o.Position,Size=V(.3,.3,.3),Transparency=1}):Play()end)
task.wait(.03)end end)end
local function psh(o)
task.spawn(function()
for i=1,25 do
if not o or not o.Parent then break end
task.spawn(function()
local sz=math.random(15,40)/10
local p=Instance.new("Part",workspace)
p.Size=V(sz,sz,sz)p.Position=o.Position
p.Anchored=true p.CanCollide=false p.Material=Enum.Material.Neon
p.Color=C(255,math.random(50,120),math.random(50,120))
p.Transparency=.2 ef[#ef+1]=p
local a=math.random()*math.pi*2 d=math.random(25,65)
T:Create(p,TweenInfo.new(.9),{Position=o.Position+V(math.cos(a)*d,math.random(-20,20),math.sin(a)*d),Size=V(.3,.3,.3),Transparency=1}):Play()end)
task.wait(.03)end end)end
local function clr()
for _,e in ipairs(ef)do if e and e.Parent then e:Destroy()end end
ef={}end
local function bm(ep,col)
local b=Instance.new("Part",workspace)
b.Shape=Enum.PartType.Ball b.Size=V(5,5,5)b.Position=ep
b.Anchored=true b.CanCollide=false b.Material=Enum.Material.Neon
b.Color=col b.Transparency=.1
local l=Instance.new("PointLight",b)l.Color=col l.Brightness=40 l.Range=100
ef[#ef+1]=b
T:Create(b,TweenInfo.new(1),{Size=V(120,120,120),Transparency=1}):Play()
for i=1,5 do
local r=Instance.new("Part",workspace)
r.Shape=Enum.PartType.Cylinder r.Size=V(.5,10,10)r.Position=ep
r.Anchored=true r.CanCollide=false r.Material=Enum.Material.Neon
r.Color=col r.Transparency=.2
r.CFrame=CFrame.new(ep)*CFrame.Angles(math.rad(90),0,0)
ef[#ef+1]=r
T:Create(r,TweenInfo.new(1.5),{Size=V(.5,180,180),Transparency=1}):Play()
task.wait(.06)end
for i=1,30 do
task.spawn(function()
local a=math.random()*math.pi*2
local d=V(math.cos(a),math.random(-1,1),math.sin(a)).Unit
local p=Instance.new("Part",workspace)
p.Shape=Enum.PartType.Ball sz=math.random(1,3)
p.Size=V(sz,sz,sz)p.Position=ep
p.Anchored=true p.CanCollide=false p.Material=Enum.Material.Neon
p.Color=col p.Transparency=.15 ef[#ef+1]=p
T:Create(p,TweenInfo.new(.9),{Position=ep+d*math.random(50,130),Size=V(.3,.3,.3),Transparency=1}):Play()
task.delay(1,function()if p.Parent then p:Destroy()end end)end)end end
local function blu()
if sAct or not ch or not ch.Parent or not ro or not ro.Parent then return end
sAct=true print("[HTT] Blue")
local fd=ro.CFrame.LookVector
local up=ro.CFrame.UpVector
local ct=ro.Position+up*3
local sp=Instance.new("Part",workspace)
sp.Shape=Enum.PartType.Cylinder sp.Size=V(.1,.1,.1)
sp.Material=Enum.Material.Neon sp.Color=C(20,80,220)
sp.Anchored=true sp.CanCollide=false sp.Transparency=1
sp.CFrame=CFrame.new(ct,ct+fd)*CFrame.Angles(0,math.rad(90),0)
ef[#ef+1]=sp
local sl=Instance.new("PointLight",sp)sl.Color=C(30,120,255)sl.Brightness=0 sl.Range=0
local hl=Instance.new("Part",workspace)
hl.Shape=Enum.PartType.Cylinder hl.Size=V(.3,.5,.5)
hl.Material=Enum.Material.Neon hl.Color=C(50,150,255)
hl.Anchored=true hl.CanCollide=false hl.Transparency=1
hl.CFrame=CFrame.new(ct,ct+fd)*CFrame.Angles(0,math.rad(90),0)
ef[#ef+1]=hl
task.spawn(function()
for k=1,20 do
if not sAct or not sp.Parent then break end
task.spawn(function()
local a=math.random()*math.pi*2 d=math.random(15,40)
local og=ct+V(math.cos(a)*d,math.random(-10,10),math.sin(a)*d)
local pp=og
for i=1,6 do
local r=i/6
local np=pp+(ct-pp)*r*.4+V(math.random(-1,1),math.random(-1,1),math.random(-1,1))
local sg=Instance.new("Part",workspace)
sg.Size=V(.4,.4,(np-pp).Magnitude)sg.CFrame=CFrame.new((pp+np)/2,np)
sg.Anchored=true sg.CanCollide=false sg.Material=Enum.Material.Neon
sg.Color=C(40,120,255)sg.Transparency=.2
local lt=Instance.new("PointLight",sg)lt.Color=C(50,150,255)lt.Brightness=4 lt.Range=15
ef[#ef+1]=sg
task.delay(.4,function()if sg.Parent then sg:Destroy()end end)
pp=np end end)
task.wait(.1)end end)
T:Create(sp,TweenInfo.new(2),{Size=V(18,.8,.8),Transparency=0}):Play()
T:Create(hl,TweenInfo.new(2),{Size=V(.5,4,4),Transparency=.3}):Play()
task.spawn(function()
for i=1,40 do sl.Brightness=i*.5 sl.Range=i*2 task.wait(.05)end end)
shk(2,.3)task.wait(2)
if not sAct or not sp.Parent then sAct=false clr()return end
local st=tick() dur=5 rad=12
task.spawn(function()
while sAct and sp.Parent do
hl.CFrame=CFrame.new(sp.Position,sp.Position+fd)*CFrame.Angles(0,math.rad(90),tick()*8)
task.wait(.02)end end)
task.spawn(function()
while sAct and ch and ch.Parent and ro and ro.Parent do
local t=tick()-st
if t>dur then break end
local a=t*1.8
local yy=math.sin(t*2)*2
local ps=ro.Position+V(math.cos(a)*rad,2+yy,math.sin(a)*rad)
local tg=V(-math.sin(a),0,math.cos(a)).Unit
sp.CFrame=CFrame.new(ps,ps+tg)*CFrame.Angles(0,math.rad(90),0)
if math.floor(t*20)~=math.floor((t-.05)*20)then
task.spawn(function()
for k=1,2 do
local an=math.random()*math.pi*2 di=math.random(20,50)hh=math.random(-15,15)
local og=ro.Position+V(math.cos(an)*di,hh,math.sin(an)*di)
local r2=workspace:Raycast(og,V(0,-80,0),rp)
local gy=r2 and r2.Position.Y or og.Y
local rk=Instance.new("Part",workspace)
rk.Size=V(math.random(15,35)/10,math.random(15,30)/10,math.random(15,35)/10)
rk.Position=V(og.X,gy+.5,og.Z)
rk.Anchored=true rk.CanCollide=false rk.Material=Enum.Material.Slate
local sh=math.random()
rk.Color=sh<.4 and C(90,60,40)or(sh<.7 and C(70,50,35)or C(110,80,55))
rk.CFrame=CFrame.new(rk.Position)*CFrame.Angles(math.random()*math.pi*2,math.random()*math.pi*2,math.random()*math.pi*2)
ef[#ef+1]=rk
T:Create(rk,TweenInfo.new(.5+math.random()*.3),{Position=sp.Position,Size=V(.3,.3,.3),Transparency=1}):Play()
task.delay(1,function()if rk.Parent then rk:Destroy()end end)end end)end
if math.floor(t*15)~=math.floor((t-.05)*15)then
task.spawn(function()
for k=1,3 do
local aa=(k/3)*math.pi*2+t*6
local p=Instance.new("Part",workspace)
p.Shape=Enum.PartType.Ball p.Size=V(.8,.8,.8)
p.Anchored=true p.CanCollide=false p.Material=Enum.Material.Neon
p.Color=C(math.random(20,60),math.random(80,150),255)p.Transparency=.1
p.Position=sp.Position+V(math.cos(aa)*2,math.sin(aa*2)*1.5,math.sin(aa)*2)
ef[#ef+1]=p
local lt=Instance.new("PointLight",p)lt.Color=C(30,120,255)lt.Brightness=5 lt.Range=12
T:Create(p,TweenInfo.new(.5),{Transparency=1,Size=V(.1,.1,.1)}):Play()
task.delay(.6,function()if p.Parent then p:Destroy()end end)end end)end
task.wait(.03)end end)
task.wait(dur+.3)sAct=false
if sp.Parent then
local ep=sp.Position
bm(ep,C(30,120,255))
shk(1.2,1.5)drt(ep,40)drtC(ep,1.5,.2)stm(ep,1)end
task.wait(1)
if sp.Parent then sp:Destroy()end
if hl.Parent then hl:Destroy()end
task.wait(.5)clr()print("[HTT] Blue done")end
local function prp()
if cast or not ch or not ch.Parent or not ro or not ro.Parent then return end
cast=true kk()task.wait(.8)
if not ro.Parent then cast=false rk()return end
local fd=ro.CFrame.LookVector
local rt=ro.CFrame.RightVector
local up=ro.CFrame.UpVector
local cs=ro.Position+fd*1.5+up*1
drt(ro.Position,25)
local bp=cs+rt*5-fd*3+up*1
local rp2=cs-rt*5-fd*3+up*1
local oB=orb(bp,C(60,160,255),.1)
local oR=orb(rp2,C(255,40,60),.1)
oB.Transparency=1 oR.Transparency=1
local lB=oB:FindFirstChildOfClass("PointLight")
local lR=oR:FindFirstChildOfClass("PointLight")
T:Create(oB,TweenInfo.new(2),{Size=V(3,3,3),Transparency=0}):Play()
T:Create(oR,TweenInfo.new(2),{Size=V(3,3,3),Transparency=0}):Play()
task.spawn(function()
for i=1,20 do
if lB then lB.Brightness=i*.5 lB.Range=i*1.5 end
if lR then lR.Brightness=i*.5 lR.Range=i*1.5 end
task.wait(.1)end end)
local rB=rng(bp,C(150,220,255),.5)
local rR=rng(rp2,C(255,150,150),.5)
rB.Transparency=1 rR.Transparency=1
T:Create(rB,TweenInfo.new(2),{Size=V(.3,8,8),Transparency=.3}):Play()
T:Create(rR,TweenInfo.new(2),{Size=V(.3,8,8),Transparency=.3}):Play()
shk(2,.15)
task.spawn(function()
while oB and oB.Parent do
rB.CFrame=CFrame.new(oB.Position)*CFrame.Angles(tick()*8,tick()*6,math.rad(90))
task.wait(.02)end
if rB.Parent then rB:Destroy()end end)
task.spawn(function()
while oR and oR.Parent do
rR.CFrame=CFrame.new(oR.Position)*CFrame.Angles(-tick()*8,tick()*6,math.rad(90))
task.wait(.02)end
if rR.Parent then rR:Destroy()end end)
task.wait(2)
pul(oB)psh(oR)stm(ro.Position,3.5)
T:Create(oB,TweenInfo.new(1),{Size=V(6,6,6)}):Play()
T:Create(oR,TweenInfo.new(1),{Size=V(6,6,6)}):Play()
task.wait(1)
if not ro.Parent or not oB.Parent or not oR.Parent then cast=false rk()clr()return end
local md=ro.Position+fd*4+up*1.5
T:Create(oB,TweenInfo.new(.7),{Position=md}):Play()
T:Create(oR,TweenInfo.new(.7),{Position=md}):Play()
task.wait(1)
if oB.Parent then oB:Destroy()end
if oR.Parent then oR:Destroy()end
local oP=orb(md,C(180,0,255),1)
oP.Transparency=1
local lP=oP:FindFirstChildOfClass("PointLight")
T:Create(oP,TweenInfo.new(.6),{Size=V(10,10,10),Transparency=0}):Play()
if lP then lP.Brightness=25 lP.Range=70 end
shk(1.5,1.2)task.wait(.4)shk(1,.6)
local hh=rng(md,C(220,100,255),25)
task.spawn(function()
while oP and oP.Parent do
hh.CFrame=CFrame.new(oP.Position)*CFrame.Angles(tick()*5,tick()*4,math.rad(90))
task.wait(.02)end
if hh.Parent then hh:Destroy()end end)
task.spawn(function()
for i=1,6 do
if not oP.Parent then break end
oP.Size=V(12,12,12)task.wait(.08)
oP.Size=V(9,9,9)task.wait(.08)end end)
task.wait(1.2)
if oP.Parent then
local fp=oP.Position dir=fd BM=350 N=35
bm(fp,C(220,100,255))
shk(1.5,1.8)drt(fp,60)drtC(fp,3,.15)
task.spawn(function()
for k=1,3 do
task.wait(.15)
if not ro.Parent then break end
spr(fp+V(math.random(-15,15),math.random(-5,10),math.random(-15,15)),dir)end end)
task.spawn(function()
for i=1,N do
if not ro.Parent then break end
local d=(i/N)*BM pos=fp+dir*d sz=15-(i/N)*8
local c=Instance.new("Part",workspace)
c.Shape=Enum.PartType.Ball c.Size=V(sz,sz,sz)c.Position=pos
c.Anchored=true c.CanCollide=false c.Material=Enum.Material.Neon
c.Color=C(200,50,255)c.Transparency=.1
local l=Instance.new("PointLight",c)l.Color=C(200,80,255)l.Brightness=15 l.Range=45
ef[#ef+1]=c
task.delay(1.5,function()if c.Parent then c:Destroy()end end)
task.wait(.015)end end)
drt(ro.Position,40)task.wait(.5)
local ep=fp+dir*BM
bm(ep,C(220,100,255))shk(1.5,2)stm(ep,1.5)drt(ep,60)drtC(ep,2.5,.2)end
task.wait(3)
if oP and oP.Parent then oP:Destroy()end
rk()task.wait(.4)clr()cast=false print("[HTT] Purple done")end
bC.MouseButton1Click:Connect(function()
if cast then return end
bC.Text="CASTING..."
task.spawn(function()prp()bC.Text="CAST PURPLE"end)end)
bS.MouseButton1Click:Connect(function()
if sAct then return end
bS.Text="SUMMONING..."
task.spawn(function()blu()bS.Text="BLUE SPEAR"end)end)
task.spawn(function()
while true do
task.wait(1)
if auto and not cast and ch and ch.Parent and ro and ro.Parent then prp()end end end)
bA.MouseButton1Click:Connect(function()
auto=not auto
bA.Text=auto and "AUTO: ON"or "AUTO: OFF"
bA.BackgroundColor3=auto and C(30,120,60)or C(60,60,60)end)
U.InputBegan:Connect(function(i,gp)
if gp then return end
if i.KeyCode==Enum.KeyCode.V and not cast then
bC.Text="CASTING..."
task.spawn(function()prp()bC.Text="CAST PURPLE"end)end
if i.KeyCode==Enum.KeyCode.B and not sAct then
bS.Text="SUMMONING..."
task.spawn(function()blu()bS.Text="BLUE SPEAR"end)end end)
local function onCh(c)
ch=c
local hu=c:WaitForChild("Humanoid")
ro=c:WaitForChild("HumanoidRootPart")
cast=false pose=false sAct=false clr()
print("[HTT] Ready")
hu.Died:Connect(function()
cast=false pose=false auto=false sAct=false clr()
bA.Text="AUTO: OFF"bA.BackgroundColor3=C(60,60,60)end)end
pl.CharacterAdded:Connect(onCh)
if pl.Character then onCh(pl.Character)else task.spawn(function()onCh(pl.CharacterAdded:Wait())end)end
print("[HTT] Loaded - V=Purple B=Blue")
