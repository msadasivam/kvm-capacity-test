# kvm-capacity-test
Apigee Edge KVM (CPS enabled) scales well. This is a test harness including a test proxy and a JMeter testcase to gain confidence and measure performance when using KVM as a store for considerable volume/size of entries.

## Test
This is a hacky effort.

Pick
1) JMeter 3.1
2) Apigee Edge org

Steps
- Deploy API in your org
- Update org host in JMeter tests - 2 places that make the HTTP request
- Enable Store Thread group
- Update Counter start value for seq
- Update thread count and iterations to the required number of KVM entries
- Run test. One call creates one entry like so
        {seq} = str1,system.time,str2,str3,{seq}
- When test is done, disable Store and enable Query
- Adjust Random start and End to cover the entries created
- Assertion checks for response size 160 bytes. When less than 160 bytes KVM doesn't have a value.