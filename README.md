
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




|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||

The Below image show Full Process Of Master Plane And Workload Plane

![Screenshot 2024-09-18 235955](https://github.com/user-attachments/assets/036a30f5-0b76-4749-b41a-89bef764649b)
