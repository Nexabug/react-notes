# A First Look At React

in this section ham log dekhnge ki 
- [Why Do Front-End Frameworks Exist?](##why-do-front-end-frameworks-exists?)
- [react vs vanilla js](##react-vs-vanilla-js)
- [what is react?](##what-is-react?)
- How to create the react project?

## Why Do Front-End Frameworks Exist

pahle ke samy me jab website sever side wali hoti thi to hame website ke code server se milta tha then wo code hamre website(clinte-side) pe aa kar lag jata tha

iska example wordpress hai
yaha pe rendering server side ho rahi hai

![server-side](https://github.com/user-attachments/assets/e3b6e8ab-48a7-4a14-9795-5770055681b3)

but now ab ham server se code ki jagh api se code lete hai jo clinte-side pe aake render hota hai so isse hi single page application kahte hai jo ek page me hi sara data rakhe and bina reload ke intrect kare user se

![clinte-side](https://github.com/user-attachments/assets/4fab1293-6f9c-4e1d-a531-cc11008bdc74)

### why we can't build a singel-page app in vanilla js?

- agar ham karna bhi chahe to bahut sare code ka mess ban jayega
- ye ui ko data se syunc nhi rakh pata hai har
- wahi react data ko ui se sync rakhta hai bina kisis reload ke
- harder to understand and create more bug

so final ans yah hai ki hame framework ki jarurat isliye padti hai kyuki isse ham data ko ui se sync rakh skte hai (and react bhi ek framework hi hai jo javascript ko apna base manti hai) 

## react vs vanilla js

- code ka mess jyada nhi hota hai
- hame vanilla js me ek ek step bata kar karna hota hai like(how to do it?)
- wahi hame react me (what to do ?) batana hota hai

## what is react?

so ye ek js ki libary hai

![what is react](https://github.com/user-attachments/assets/256baf30-d8ac-49a5-9f85-d39da74f7f30)

### based on components
so componet react ki ek buliding blocks hai ham webpage ko agal alag component me bana kar usko render kara te hai hai clinde side pe we can under stand by a logo-puzzule example sabhi chote chote comoponents se mil kar ek full logo ban jata hai

![componets](https://github.com/user-attachments/assets/f17f30db-0878-4be6-a57a-f40b85d66e30)

### declerative
- so ham componets ko JSX syntax me likh kar dalte hai
- and ye hame ye bata haiki comopnent kaisa dikhna chahiye based on current data
- react ko banya hai isliye gya hai ki hame(devlopers) ko kabhi bhi DOM(document object model) ko directly toch na karna pade
- JSX ek syntax hota hai jisme ham css, html ,js ke parts laga skte hai and other components ko bhi refreance kar skta hai

### state-driven

so agar ham kabhi dom ko toch hi nhi karenge to ham change kaise karenge?

so uske liye state ka use karte hai jisse hota hai yah ki jaise hi ham kuch bhi state me change karte hai ui bhi us ke according change hota hai kyuki wo ui se directly sync hota hai

isliye to hai react ko react kahte hai kyuki wo react karta hai

## How to create the react project?

so react project ko banane ke liye hame cmd me ja kar

```bash
npx create-react-app fileName
```

and agar apko project ko Start karna hai means local Host pe chalna hai to hame new terminal (vs code) me ja kar ye likhan hai then wo local Host me khul jayega 

```
npm run start
```
