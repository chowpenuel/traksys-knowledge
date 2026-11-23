# Splitting Storage Transfers on ID

*Source: https://portal.parsec-corp.com/hc/en-us/articles/230664567-Splitting-Storage-Transfers-on-ID*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

In order to split transfers, multiple products must be stored in the same Storage System. Transfers split when a Transfer Out is triggered for an amount of a Product that is greater than the amount that is available. When this happens, the Product is completely emptied from the Storage System and a different Product is emptied out for the remaining amount. Transfer splits can be observed through the `tTransfer` and `tSystemStorage` tables.

### **Example and****Explanation**

A single Storage System will be receiving transfers of two different Products. There will be 1000 kg of the first Product and 500 kg of a second Product. When the transfers are initiated, both of the transfer entries will appear in the `tTransfer` table.

![](https://portal.parsec-corp.com/hc/en-us/article_attachments/115013442187/92d15b36aade82633ca2d986c55f62d75ecf5e35fef7c31602d02d29a3a11346.png)

![](https://portal.parsec-corp.com/hc/en-us/article_attachments/115013442207/3a7e94adfa550bf0a627fe802c05c44a308ffcced1cc0330ecb1e64cb560f420.png)

In the `tSystemStorage` table, two separate entries for the same system will appear. In the image below, the SystemID is the same in both entries, but the ProductID and Quantity fields are different. This shows that both transfers are using the same System, but have different Products and different quantities of each Product.

![](https://portal.parsec-corp.com/hc/en-us/article_attachments/115013442227/2f075c7af06d89299030afd54d11d43499949cc70a019b0a3c05d80cea22c36d.png)

Later on, a Transfer Out is triggered for 1200 kg of the first Product, even though there is only 1000 kg currently in storage. In this situation, all 1000 kg of the first Product will be emptied out. Since 200 kg of Product still needs to be emptied, the process will continue by emptying out 200 kg of the second Product.

Since two types of Products are emptied out, two separate entries will be created for each Product. Both Products will also share a common SplitTransferID, because they were part of the same Transfer Out. The SplitTransferID will always have the same ID as the parent ProductID that was transferred. Since the first Product was the desired Product, the SplitTransferID was given a value of 60.

![](https://portal.parsec-corp.com/hc/en-us/article_attachments/115013442247/49501390f647afc30af36e82063a68ee42aa1de1f2a87c36c8b397f507eb5ed2.png)

![](https://portal.parsec-corp.com/hc/en-us/article_attachments/115013442267/a07f938b9dea4d80622aef64ceac49d9cfe48d7cabc0a1e6d5d78f68102f9d0e.png)

In the `tSystemStorage` table, the entry for the first Product will disappear because it was fully emptied out. The entry for the second Product will still show a remaining storage value of 300 kg since 200 kg was emptied out by the transfer.

![](https://portal.parsec-corp.com/hc/en-us/article_attachments/115013442287/46ddb8ec4ce9b41f35c84f3a143fa6b1069d89fac03ff82e43d7d0a14c71dccf.png)
