# 🌐 Kubernetes Network Policies

A hands-on walkthrough for understanding, analyzing, and creating **NetworkPolicies** in Kubernetes — to control pod-to-pod communication using labels and egress/ingress rules.

---

## 📘 Step 1 – Inspecting an Existing Network Policy

**We start by examining an existing NetworkPolicy to understand its structure and scope.**

<br><br>

<p align="center">
  <img width="295" height="52" alt="existing network policy" src="https://github.com/user-attachments/assets/7d378634-9a3d-4639-a38a-9c53baa171b2" />
</p>

<br><br>

---

## 🧩 Step 2 – Listing All Pods

**Before analyzing which pods are affected, let’s list all pods in the namespace.**  
This helps identify potential matches with the policy’s selector.

<br><br>

<p align="center">
  <img width="381" height="106" alt="list pods" src="https://github.com/user-attachments/assets/f690f707-fba6-47d7-bf37-6d11958ab511" />
</p>

<br><br>

---

## 🔍 Step 3 – Checking the Policy’s Label Selector

**To find which pods the policy applies to, we check the labels defined under `podSelector` in the policy’s YAML.**

<br><br>

<p align="center">
  <img width="493" height="469" alt="policy labels" src="https://github.com/user-attachments/assets/1b5948dd-a46f-428d-9791-c5f412d03f14" />
</p>

<br><br>

---

## 🏷️ Step 4 – Matching Pods to Labels

**We compare the selector labels with our pods to identify which pod(s) the NetworkPolicy affects.**

<br><br>

<p align="center">
  <img width="1068" height="391" alt="matching pod labels" src="https://github.com/user-attachments/assets/a0d74a69-126d-44ac-94c2-186a84ced255" />
</p>

<br><br>

✅ **Conclusion:** The NetworkPolicy applies to the **`payroll` application** pods.

---

## 🚧 Step 5 – Designing a New Network Policy

**Goal:**  
Allow **egress traffic** from the `internal` application **only to** the following services:
- `payroll-service`
- `db-service`

We’ll reference Kubernetes documentation and construct the YAML carefully, ensuring the **labels and selectors** match the target pods.

<br><br>

<p align="center">
  <img width="307" height="481" alt="egress network policy yaml" src="https://github.com/user-attachments/assets/48a2e457-fbc2-4b8f-93da-21129ca44b09" />
</p>

<br><br>

---

## 🧾 Step 6 – Applying  the Policy

**After applying the policy, we confirm that only the allowed egress destinations are accessible from the internal app.**

<br><br>

<p align="center">
  <img width="416" height="86" alt="policy applied" src="https://github.com/user-attachments/assets/226774ba-10ad-407b-9ac0-df7012853a95" />
</p>

<br><br>

---
Veriification will mostly come next.

## 🧠 Key Takeaways

- **NetworkPolicies** control which pods can communicate with which — both **Ingress** and **Egress**.  
- They use **labels** to select target pods, not pod names.  
- By default, when a NetworkPolicy is applied, **all traffic is denied** unless explicitly allowed.  
- Always test communication after applying a policy using `kubectl exec` or `curl` from inside pods.  

---

<p align="center"><b>With the right NetworkPolicies, you gain fine-grained control and enhanced security for Kubernetes workloads.</b></p>
