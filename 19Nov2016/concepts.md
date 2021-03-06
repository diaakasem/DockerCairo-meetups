**Basic Consensus concepts**
---------------------------

  - Leader election algorithm must satisfy the following:
   
    1. Elect one leader only among the **non-faulty processes**
    2. All non-faulty processes agree on who is the leader
   
  - Most popular Leader election algorithms:
 
  The most popular election algorithms can be classified into multiple categories, a classical leader election protocols such
  as (Ring protocol/algorithm), Paxos-like or (Zab) approaches such as zookeeper and Raft consensus protocol such as Consul.
  
   1. **Ring** 
   
       ![Alt text](images/Ring-LeaderElection.png "Ring Leader Election Algorithm")
      
      * N processes/nodes are organized in a logical ring.
      * Any node can initiate election in case of leader failure.
      * Each node send message to its successor containing the leader ID.
      * If the current Node has a higher ID .. change the leader ID to current node ID.
      * If the first node (that initiated the election) recieves the highest ID, then it 
      send a message to all nodes containing the elected leader.
      
      
   2. **Google CHUBBY**
   
      - group of replicas need to have a master by following:
   
      ![Alt text](images/google-chu.png "Google Chubby Leader Election Algorithm")
      
      * Potential leader tries to get votes from other servers
      * Each server votes for at most one leader
      * Server with majority of votes becomes new leader, informs everyone
      * Master node run election again after a period called *Master lease*
      
   3. **Zookeeper**
   
      * Apply Paxos-like protocol!
      * Each Server monitors its next higher server id
      * If that successor was the leader and it has failed.... become a new leader
      * Else: wait timeout and check successor again.

   4. **Consul**
      
      * First check out this great website discussing Raft Algorithm in details [TheSecretLivesOfData.com](http://thesecretlivesofdata.com/raft/)
      * Consul uses Raft consensus algorithm, in order to maintian the fault-tolerance.
      * Each server has a state machine and log "hash table".
      * Get a command from log and check if that state machine still the same on all servers even after applying multiple commands.
      * "As a result, each state machine processes the same series of commands and thus produces the same series of results 
       and arrives at the same series of states." you can read more about from [here](https://raft.github.io/)
       
       
**Sources**

1. [Raft Consensus Algorithm](https://raft.github.io/raft.pdf)
2. [Zab vs Paxos](https://cwiki.apache.org/confluence/display/ZOOKEEPER/Zab+vs.+Paxos)
3. [Ring Leader Election Algorithm](http://www.cs.rug.nl/~eirini/DS_slides/leader_election.pdf)
4. [Google Chubby Qourum "video"](https://www.coursera.org/learn/cloud-computing-2/lecture/IDKhR/1-3-election-in-chubby-and-zookeeper)
