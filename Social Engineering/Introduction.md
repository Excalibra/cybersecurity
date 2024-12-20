# Introduction to Social Engineering

## Type of Social Engineering attacks

I want to stress that we don't use these individually. So, for example, I wouldn't just use elicitation. I wouldn't just use interrogation. I want to use a combination because that's going to help me be a much better individual doing social engineering.

### Three Components of Social Engineering 

- Elicitation: So elicitation is basically when an attacker uses open-ended questions to try to get more information about the victim. So if you think of this as a salesperson, and I’m a salesperson, I call up a potential customer and I'm on the phone with them, and rather than asking them, "Do you like your current service provider?"—which is a yes or no question, a closed-ended question—what I want to do instead is ask them open-ended questions.

  So what I might ask them is, "What kinds of things don’t you like about your current service provider?" or "What kinds of challenges do you have that your current service provider’s not meeting?" And you see how that’s open-ended? It allows them to answer more than just yes or no. They’re able to give us more information about that particular issue.

  So we want to do the same thing here in social engineering. Instead of asking somebody, "Does your company use Windows servers?"—that’s a yes or no question, a closed-ended question—I might ask instead, "Hey, have you guys ever had any trouble in your company migrating to Azure, or have you had any cloud migration issues, et cetera?" Right? They might say, "Yeah, our Azure has been a problem because a lot of organizations are multi-cloud right now." They might specify what the issue is. They might say, "Yeah, we’ve had some trouble with misconfigured S3 buckets." Well, you know right away that’s AWS, and that’s S3 buckets.

  So guess what? You might have just found a way into that company. Right? So that’s why we do elicitation.

- Interrogation: Interrogation, as the name implies, is when we're asking questions. A key point here is the body language, where we're normally in person or maybe on video chat with them, but traditionally it's in person. We're reading the body language and looking at any type of gestures they do. Are they moving their hands? Are they stomping their feet? Does their eyebrow twitch? Are they blinking a lot? Are they sweating? Are they rubbing their hands? What kind of facial expressions do they have? Are they frowning? Are they smiling? Do they do a certain thing or look a certain way when they’re speaking certain things? These are all clues that can help us determine if they’re lying about something and if there’s more information they would like to share but aren’t sharing yet.

- Pretexting: Then there's pretexting, which is basically us giving false information to get more information. For example, let’s say I pretend I’m a delivery driver for Uber Eats, DoorDash, or one of these food delivery companies. I go to the front desk of a company, and my goal is to get past the receptionist, the gatekeeper. I might say, “I’ve got food for Sally Smith in accounting.” They might say there’s no Sally Smith, or maybe they tell me there is a Sally in accounting. I could have a receipt with someone named Sally, but the last name is crossed out. Then I could say, “I’ve got food for Sally in accounting. Can I take it to her?” If they ask, “Who’s Sally?” or “What’s her last name?” I might say, “I don’t know, see the receipt?” and then continue saying, “I’m just trying to deliver food, what can I do? How can you help me?” My real goal is to get into the company or gather more information from someone. That’s what pretexting is.

## Components of Social Engineering

There are different types of social engineering. I want to stress that this is not going to be an all-inclusive list, at least not on the bullet points, but we’ll cover the main areas of social engineering.

- Phishing: So basically, phishing, which you might have heard about, is essentially getting someone to take the action that you want them to take. This can be done via email, which is the most common form of phishing that you’re probably going to see, or through text messaging, which is called SMS phishing, or even through the phone, which is known as vishing (voice phishing).

The goal of phishing is to get someone to take an action, such as giving you information, clicking on something to get their login credentials, downloading something to spread malware on the company’s systems, or taking an action like wiring you money because you pose as a CEO and say it’s urgent.

- Spear Phishing: Another thing is spear phishing, which is a targeted attack. While phishing might be a broad blast of emails saying something like, "Hey, your Amazon account is locked out, click this link to log in and change your password," which could go out to millions of people, spear phishing is more specific. For example, you might target one person, like Ken, and try to get him to click a link, or target everyone at a specific company, like a healthcare company, to get them to take a particular action.

- Whaling: When we talk about whaling, we're referring to targeting high-profile individuals, like senior executives. This is more focused on the "big fish" level, like CEOs or CFOs, and the goal is to get them to take some kind of action. So maybe we target the CEO or the CFO or someone like that.

- Pharming: Farming is basically where I type in, for example, Google.com, and instead of going to Google.com, I actually get redirected to a malicious site. But that still looks like Google.com. So that's all we're doing with that. That's a DNS cache poisoning attack. And we're basically just redirecting them to a malicious website or some other website besides the real website.
  
- Hoaxing: Hoaxing, many people probably got this way back in the day. That's where they'll send the email, kind of those chain letter emails. Right? If you send this to a million people, you make a million bucks. Or the other thing is maybe, hey, there's a new virus, spread this around, share with your friends, protect everybody. By the way, click the link to download it, update to fix a virus. Right.

- Shouolder Surfing: Shoulder surfing, as the name implies, is when someone is looking over your shoulder to gather information. This could happen in public spaces like cafes, airports, or even on public transportation, where someone might observe you entering your PIN, typing a password, or reading sensitive information on your screen.
  
- Baiting: Baiting is a social engineering technique where attackers lure individuals into taking an action that will compromise their security. One common example is USB drop attacks, where attackers distribute USB drives in places like company parking lots or public areas, hoping that someone will find one and plug it into their computer out of curiosity or to see who the device belongs to. Once the USB is plugged in, it can spread malware or gain unauthorized access to the computer or network. This method exploits human curiosity to deliver malicious payloads.

- Tailgating: Baiting is a social engineering technique where attackers lure individuals into taking an action that will compromise their security. One common example is USB drop attacks, where attackers distribute USB drives in places like company parking lots or public areas, hoping that someone will find one and plug it into their computer out of curiosity or to see who the device belongs to. Once the USB is plugged in, it can spread malware or gain unauthorized access to the computer or network. This method exploits human curiosity to deliver malicious payloads.

## Behaviour Controls

We will focus specifically on both behavioural measures and technical controls, as human error remains the weakest link in security. By changing behaviours, we can significantly enhance our defences against social engineering attacks.

As mentioned, our discussion will cover both behavioural and technical controls. 


![image-removebg-preview(2)](https://github.com/user-attachments/assets/28bd9b09-fc36-4800-992d-bfb677f34903)


### Behavioural controls

A key principle to instil in people is simple: If you didn’t request it, don’t click on it.

Consider an example from the healthcare sector. Clinicians—nurses, doctors, and other medical professionals—often prioritise patient care above all else. When security protocols are introduced, they may view them as an inconvenience or distraction from their primary responsibilities. Advice like “Don’t click on suspicious links” or “Avoid using the same password across systems” can sometimes fall on deaf ears because it doesn’t seem relevant to their daily challenges.

Now imagine approaching this issue differently. Instead of focusing on abstract security risks, the messaging could be tied directly to their specific concerns. For instance:

- How a phishing attack could lock them out of systems, delaying access to patient records,
- How it might prevent them from completing charting in time for a break, or
- How it could delay critical care by disrupting their workflow.

By framing security in terms of how it directly affects their ability to provide care and complete their work efficiently, the advice becomes far more impactful.

The results of such an approach could be profound. Staff might become more receptive to the importance of security and start adopting safer behaviours. For example, in one case, a new CEO sent out a company-wide survey. This seemingly benign email led to a flood of queries from vigilant nurses, worried it might be a phishing attack. Their heightened awareness and suspicion—even towards legitimate emails—were a direct result of behavioural changes encouraged through relatable security messaging.

While the extra workload from addressing these queries could be challenging, it would ultimately reflect a successful outcome. Staff would have internalised the importance of caution and applied it consistently, demonstrating a shift in their overall approach to security.

This example highlights the importance of tailoring behavioural controls to the unique priorities and concerns of end users.

On the technical side, particularly for penetration testers, it’s useful to think about the daily activities of the individuals you’re trying to target. For example:

- How might you bypass their validation of a link?
- How could you persuade them to click your link instead of navigating to a legitimate website?

Understanding these details benefits both defensive and offensive strategies. On the defensive side, you gain insight into how protocols impact workflows and behaviour. On the offensive side, you can identify psychological techniques to exploit potential weaknesses.

Ultimately, social engineering is a psychological game. By addressing both technical measures and user behaviour, we can build stronger defences and better anticipate potential attacks.

### Link Validation Practices

**1. Use Online Tools:**

Services like VirusTotal.com can analyze a URL for potential malware or suspicious activity before you click on it.

**2. Identify Homograph Attacks:**

Look for deceptive URL spellings (e.g., g00gle.com instead of google.com) that exploit similarities between characters like the number 1 and the lowercase letter l.
Fonts in emails or websites can make these distinctions even harder to notice.

**3. Hidden URLs:**

Be cautious of links embedded in buttons or text, as their actual destination may differ.
Hovering over links on a computer can reveal the real destination, but this feature is often unavailable on mobile devices.

**4. Mobile Device Challenges:**

Mobile interfaces often lack hover-over functionality, making it harder to inspect links.
Solution: Copy the link and paste it into a validation tool like VirusTotal to verify it before accessing.


### Best Practices for Sender Validation

**1. Verify Unusual Requests:**

If an email claims to be from a known sender but makes an unusual request (e.g., transferring money, sharing sensitive information), confirm directly with the sender.

Methods:
Call the sender on a known phone number (not one provided in the suspicious email).
Text the sender if you have a verified contact.

**2. Cross-Reference Known Communication Styles:**
Be suspicious of emails that:
Use language or tone inconsistent with the sender's typical style.
Contain grammatical errors or urgent/emotional appeals.

**3. Look for Spoofed Email Addresses:**
Check the "From" field for slight misspellings or inconsistencies (e.g., ceo@company.co vs. ceo@company.com).
Inspect the email headers to identify the originating server, which can reveal if the message was sent from an unexpected location.

**4. Establish a Verification Culture:**
Encourage team members to validate requests for sensitive actions like wire transfers or account access without fear of delaying processes.

**5. Remember the Red Flags:**
Sudden, unexpected changes in payment methods.
Messages urging immediate action without standard checks.



### Steps to Minimize Online Exposure

**1. Limit Personal Information Online:**

Avoid oversharing on social media: Remove details like your birthday, address, phone number, or vacation plans that could be exploited by attackers.
Check privacy settings: Adjust the privacy settings on all social platforms to restrict what is visible to the public.
Audit online accounts: Delete old or unused accounts that still hold your data.

**2. Verify Suspicious Links:**

Use scanning tools: Before clicking, paste links into tools like VirusTotal to check for red flags.
Manually navigate to websites: Instead of clicking links in emails (e.g., “Reset your Amazon password”), type the website address directly into your browser.

**3. Exercise Common Sense:**

Question the urgency: Phishing attempts often create a sense of panic to make you act quickly—pause and think critically.
Test for actual issues: For example, if an email claims there’s a problem with your Amazon account, log in directly on the site to verify.

**4. Educate End Users:**

Promote these behaviors within your organization:
Verify the sender.
Inspect suspicious links or attachments.
Report anything that seems off to IT or security teams.

**5. Monitor Your Digital Presence:**

Set up Google Alerts for your name or business.
Use tools to identify and remove your personal information from data brokers or public directories.


![image-removebg-preview(3)](https://github.com/user-attachments/assets/0adb3de7-e2c5-4710-8d8f-24c8e3e9d35b)


## Categorized Security Controls

**1. Sandbox**

- Isolates files or applications in a controlled environment to test for malicious activity.
- Examples:
  - BufferZone
  - Sandboxie (open-source for Windows)
  - Built-in macOS sandboxing (requires configuration)
- Purpose:
  - Prevent malicious files from affecting the main system.
  - Safely analyze unknown downloads.

**2. Endpoint Protection**

- Encompasses tools and strategies for securing individual devices (endpoints) from threats.
- Features:
  - Antivirus and anti-malware solutions.
  - Real-time monitoring for suspicious activities.
- Examples:
  - Traditional endpoint security software suites.

**3. Application/Execution Controls**

- Limits what applications or processes can run on a system.
- Features:
  - Blocks unverified applications.
  - Protects against unauthorized software execution.
- Examples:
  - Policies enforcing application behavior.
  - Tools that prevent execution based on permissions or rules.

**4. Whitelisting**

- Restricts access or execution to a predefined list of approved applications or processes.
- Benefits:
  - Prevents unauthorized software from running.
  - Offers precise control over the system's application environment.
- Challenges:
  - Requires frequent updates to the whitelist.
  - May disrupt workflows if legitimate applications are blocked.

**5. Compartmentalization**

- Segments systems, networks, or files to prevent the spread of malware.
- Examples:
  - Virtual machines or containers for isolating processes.
  - Network segmentation to separate critical systems.
- Purpose:
  - Reduces the impact of a single compromised device.
  - Ensures that malware is confined to its initial entry point.
