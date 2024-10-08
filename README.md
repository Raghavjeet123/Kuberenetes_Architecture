
  ![#_Kuberenetes_Architecture](https://github.com/user-attachments/assets/923a7760-2ee6-4e32-8e51-dab3758dea82)


Kubernetes architecture ko samajhne ke liye, humein yeh dekhna padega ki kaise yeh components milke ek reliable aur flexible environment banate hain jahan containerized workloads ko handle kiya ja sake.

----> Ek Kubernetes cluster do main parts mein divide hota hai: Control Plane Nodes aur Worker Nodes.


-------------------------------------------------------------------------Control Plane Nodes---------------------------------------------------------------
    Yeh wo nodes hote hain jo cluster ka management aur decision-making ka kaam karte hain. Inko aap cluster ke "brain" jaisa samajh lo. Iske andar kuch key components hote hain:

 -------------------------------------------![Screenshot 2024-09-18 234727](https://github.com/user-attachments/assets/940d486f-108c-4318-873f-0317e556faec)------------------------------------------


   --> API Server: Yeh wo component hai jo Kubernetes ke baaki parts ko connect karta hai. Jaise kisi app ko access karne ke liye API banate ho, waise hi Kubernetes ke control 
       plane ke saath baat karne ke liye API server use hota hai.

   --> etcd: Yeh ek distributed database hai jisme cluster ki saari information aur configurations store hoti hain. Isko aap cluster ka memory bank bol sakte ho.

   --> Controller Manager: Yeh wo process hai jo cluster ki health ko monitor karta hai aur ensure karta hai ki har cheez sahi se chal rahi ho. Jaise agar ek pod down ho jaye, 
    toh yeh naya pod start karne ka kaam karega.

   --> Scheduler: Yeh decide karta hai ki kaunsa pod kis worker node par chalega, taaki resources ka best use ho sake.




------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



 --------------------------------------------------------------------------Worker Nodes------------------------------------------------------------------
   
   Yeh nodes actual workload ko handle karte hain, yaani aapke containerized applications ko run karte hain. Worker nodes ko aap cluster ke "muscle" samajh sakte ho. Iske 
   andar kuch important parts hote hain:



---------------------------------------------![Screenshot 2024-09-18 235111](https://github.com/user-attachments/assets/e1a7cd71-86db-480d-9c4f-75e66bba32ee)---------------------------------------------

   

--> Kubelet: Har worker node par chalne wala ek process jo ensure karta hai ki pods sahi se run ho rahe hain (You can see the kubelet in the above picture). Yeh control plane ke instructions ko follow karta hai.

--> Container Runtime: Yeh actual containers ko run karta hai. 
    kubernetes popular container run times are - containerd, CRI-O, Docker Engine, Mirantis Container Runtime

--> Kube-proxy: Network traffic ko manage karta hai, taaki pods ke beech aur bahar se communication smooth rahe aslo provide ip address to the pods, in above picture you can see the kube-proxy.



_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

The Below image show Full Process Of Master Plane And Workload Plane

![Screenshot 2024-09-18 235955](https://github.com/user-attachments/assets/036a30f5-0b76-4749-b41a-89bef764649b)


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



______________________________________________________________________________How API sever gets request and do further process____________________________________________________________________

![Capture](https://github.com/user-attachments/assets/3c795069-ac8d-4d85-aa7e-b8466441a77f)

______________________________________ Below Describe the whole process how API server gets request and do futher
__________________________________________________________________________________________________________________________________________________________________________________________________
Step 1: kubectl apply -f mydeployment.yaml
Jab tum kubectl apply command chalate ho, to yeh request tumhare kubectl client se Kubernetes API Server tak jaati hai. API Server ka kaam hai ki jo request aaye, usse handle kare aur decide kare ki aage kaunse component ko kaam dena hai. Yahan tumne ek YAML file di hai jisme deployment define hai.
Is step me kubectl tumhari deployment ki desired state ko API Server ko batata hai.

__________________________________________________________________________________________________________________________________________________________________________________________________
Step 2: Writes Desired State of Deployment to etcd
........API Server ke paas jab yeh deployment ki request aati hai, to sabse pehle API Server check karta hai ki yeh deployment already exist karta hai ya nahi. Phir API Server yeh desired state 
........(jaise kitne pods chahiye, kaunsi image run karni hai) ko etcd mein store kar deta hai.
. etcd ek distributed database hai jisme Kubernetes cluster ki sari information store hoti hai.


__________________________________________________________________________________________________________________________________________________________________________________________________
Step 3: Tells Scheduler to Find a Node for the Pods
Ab jab desired state store ho jaati hai, to API Server Scheduler ko batata hai ki naye pods ko kaunsi node pe deploy karna hai. Scheduler ka kaam hai decide karna ki kaunsi node best hai naye pod ko run karne ke liye, node ke resources jaise CPU, memory ke basis pe.
.Scheduler choose karta hai node jahan pod ko run karna hai aur API Server ko batata hai.

__________________________________________________________________________________________________________________________________________________________________________________________________
Step 4: API Server Writes to etcd the Location of the Pod
Jab Scheduler node select kar leta hai, API Server fir se etcd me pod ka location store kar deta hai. Iska matlab ab pod ka schedule ho gaya hai aur uski node location decide ho gayi hai.
.etcd mein ab pod ka actual location (node ka naam) store hota hai.

__________________________________________________________________________________________________________________________________________________________________________________________________
Step 5: kubelet Watches the API Server to See if There Are Pods It Needs to Create
Har node pe ek kubelet service hoti hai jo continuously API Server ko watch karti hai. Jab API Server mein update hota hai ki koi pod us node pe create hona hai, to kubelet us information ko read karta hai aur pod ko actual node pe run karne ke liye shuru karta hai.
.Kubelet check karta hai ki uski node pe kya pod run hona hai aur fir woh pod ko start karne ke liye necessary steps leta hai.
Summary:
To overall flow yeh hai:

kubectl command request karta hai API Server se deployment ke liye.
API Server desired state ko etcd mein store karta hai.
Scheduler node select karta hai pod ke liye.
API Server etcd mein pod ki location likhta hai.
Node ka kubelet API Server ko watch karta hai aur naye pod ko create karta hai.
Is process mein API Server central communication hub hai jo sab components ko coordinate karta hai!
