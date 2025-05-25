# A First Look At React

In This Section Ham Log Dekhnge Ki 
- [Why Do Front-End Frameworks Exist?](#why-do-front-end-frameworks-exist)
- [React Vs Vanilla JS](#react-vs-vanilla-js)
- [What Is React?](#what-is-react)
- [How To Create The React Project?](#how-to-create-the-react-project)

## Why Do Front-End Frameworks Exist<a name="why-do-front-end-frameworks-exist"></a>

Pahle Ke Samay Me Jab Website Server Side Wali Hoti Thi To Hame Website Ke Code Server Se Milta Tha Then Wo Code Hamre Website(Clinte-Side) Pe Aa Kar Lag Jata Tha.

Iska Example WordPress Hai  
Yaha Pe Rendering Server Side Ho Rahi Hai.

![Server-Side](https://github.com/user-attachments/assets/e3b6e8ab-48a7-4a14-9795-5770055681b3)

But Now Ab Ham Server Se Code Ki Jagah API Se Code Lete Hai Jo Clinte-Side Pe Aake Render Hota Hai So Isse Hi Single Page Application Kahte Hai Jo Ek Page Me Hi Sara Data Rakhe And Bina Reload Ke Interact Kare User Se.

![Clinte-Side](https://github.com/user-attachments/assets/4fab1293-6f9c-4e1d-a531-cc11008bdc74)

### Why We Can't Build A Single-Page App In Vanilla JS?

- Agar Ham Karna Bhi Chahe To Bahut Sare Code Ka Mess Ban Jayega
- Ye UI Ko Data Se Sync Nahi Rakh Pata Hai Har
- Wahi React Data Ko UI Se Sync Rakhata Hai Bina Kisi Reload Ke
- Harder To Understand And Create More Bugs

So Final Ans Yah Hai Ki Hame Framework Ki Jarurat Isliye Padti Hai Kyuki Isse Ham Data Ko UI Se Sync Rakh Sakte Hai (And React Bhi Ek Framework Hi Hai Jo JavaScript Ko Apna Base Manti Hai).

## React Vs Vanilla JS<a name="react-vs-vanilla-js"></a>

- Code Ka Mess Jyada Nahi Hota Hai
- Hame Vanilla JS Me Ek Ek Step Bata Kar Karna Hota Hai Like (How To Do It?)
- Wahi Hame React Me (What To Do?) Batana Hota Hai

## What Is React?<a name="what-is-react"></a>

So Ye Ek JS Ki Library Hai.

![What Is React](https://github.com/user-attachments/assets/256baf30-d8ac-49a5-9f85-d39da74f7f30)

### Based On Components
So Component React Ki Ek Building Blocks Hai Ham Webpage Ko Alag-Alag Component Me Bana Kar Usko Render Karate Hai Hai Client Side Pe. We Can Understand By A Logo-Puzzle Example Sabhi Chote Chote Components Se Mil Kar Ek Full Logo Ban Jata Hai.

![Components](https://github.com/user-attachments/assets/f17f30db-0878-4be6-a57a-f40b85d66e30)

### Declarative
- So Ham Components Ko JSX Syntax Me Likh Kar Dalte Hai
- And Ye Hame Ye Batata Hai Ki Component Kaisa Dikhna Chahiye Based On Current Data
- React Ko Banaya Hai Isliye Gaya Hai Ki Hame (Developers) Ko Kabhi Bhi DOM(Document Object Model) Ko Directly Touch Na Karna Pade
- JSX Ek Syntax Hota Hai Jisme Ham CSS, HTML, JS Ke Parts Laga Sakte Hai And Other Components Ko Bhi Reference Kar Sakta Hai

### State-Driven

So Agar Ham Kabhi DOM Ko Touch Hi Nahi Karenge To Ham Change Kaise Karenge?

So Uske Liye State Ka Use Karte Hai Jisse Hota Hai Yah Ki Jaise Hi Ham Kuch Bhi State Me Change Karte Hai UI Bhi Uske According Change Hota Hai Kyuki Wo UI Se Directly Sync Hota Hai.

Isliye To Hai React Ko React Kahte Hai Kyuki Wo React Karta Hai.

## How To Create The React Project? <a name="how-to-create-the-react-project"></a>

So React Project Ko Banane Ke Liye Hame CMD Me Ja Kar

```bash
npx create-react-app fileName
```
And Agar Apko Project Ko Start Karna Hai Means Local Host Pe Chalna Hai To Hame New Terminal (VS Code) Me Ja Kar Ye Likhna Hai Then Wo Local Host Me Khul Jayega.

```bash
npm run start
```
