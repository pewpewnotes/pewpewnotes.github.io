

We read Foreword, understanding how the role of sysadmin has evolved and how it was needed to be changed. Google Took the initiatives with lots of PHD researchers to make sure that the system was revised and then they made it a trend out there.

`Software Engineering has this in common with having children, the labor before the birth is painful and difficult, but the labor after birth is where you actually spend most of your effort`

Quoting from the book:

SREs are Engineers. We apply principles of Computer Science and Engineering to the design and development of computing systems: Generally, large distributed Ones. Sometimes the task also involves writing tools that is building the additional pieces those systems need, Like backups or load balancing ideally so they can be reused across systems

[[Ideas]]

Three basic tasks an SRE is supposed to do:
1. Create and Build systems which will allow providing Services
2. Reliability, Most of the time of an SRE is supposed to go in maintaining reliability of a system.
3. Operating Services built on top of distributed Contributing systems.

### Chapter 1: Introduction

#### The sysadmin approach to Service Management

Sysadmin model of service
- Pros:
    1. Ease of availability of relevant talent pool

    2. Easy to Implement

- Cons
    1. Different idealogy (Devs -> Invent and Forward, Ops -> Don't break stuffs)
    2. Indirect Cost of split


Traditional style often leads to split in opinion and design, so we need a way where in both of the teams have aligned thoughts and approaches

Quoting Google:

```
Conflict isn’t an inevitable part of offering a software service. Google has chosen to run our systems with a different approach: our Site Reliability Engineering teams focus on hiring software engineers to run our products and to create systems to accomplish the work that would otherwise be performed, often manually, by sysadmins
 
```


SRE tenets:
- Availability
- Latency
- Performance
- Efficiency
- Change Management
- Monitoring
- Emergency Response
- Capacity Planning

Monitoring should not be manual intervention, but automatic. Humans should be notified only when they need to take Action
Π -> Related to in some way, it could mean anything like a multiplication, addition. But the major point is that its a part of relationship. For example, F(x^3) = f(x^2) Π f(x)

Reliability (R) = f(mean time to failure) Π f(mean time to response)

- Humans Add latency
- Thinking through and having effective playbooks reduces MTTR 3x times


