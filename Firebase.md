## utils 
``` jsx
// Import the functions you need from the SDKs you need

import { initializeApp } from "firebase/app";

import { getAuth } from "firebase/auth";

import { getFirestore } from "firebase/firestore";

// TODO: Add SDKs for Firebase products that you want to use

// https://firebase.google.com/docs/web/setup#available-libraries

  

// Your web app's Firebase configuration

const firebaseConfig = {

  apiKey: process.env.NEXT_PUBLIC_API_KEY,

  authDomain: process.env.NEXT_PUBLIC_AUTH_DOMAIN,

  projectId: process.env.NEXT_PUBLIC_PROJECT_ID,

  storageBucket: process.env.NEXT_PUBLIC_STORAGE_BUCKET,

  messagingSenderId: process.env.NEXT_PUBLIC_MESSAGING_SENDER_ID,

  appId: process.env.NEXT_PUBLIC_APP_ID,

};

  

// Initialize Firebase

const app = initializeApp(firebaseConfig);

export const auth = getAuth();

export const db = getFirestore(app);
```

## dashboard

```jsx
import { auth, db } from "../utils/firebase";
import { useAuthState } from "react-firebase-hooks/auth";
import { useRouter } from "next/router";
import { useEffect, useState } from "react";
import { collection, onSnapshot, query, where } from "firebase/firestore";
import Message from "../components/Message";

export default function Dashboard() {
  const route = useRouter();
  const [user, loading] = useAuthState(auth);
  const [posts, setPosts] = useState([]);
  // ? is user logged?
  
  const getData = async () => {
    if (loading) return;
    if (!user) return route.push("/auth/login");
    const collectionRef = collection(db, "posts");

	// special user's posts
    const q = query(collectionRef, where("user", "==", user.uid));

    const unsubscribe = onSnapshot(q, (snapshot) => {

      setPosts(snapshot.docs.map((doc) => ({ ...doc.data(), id: doc.id })));

    });

    return unsubscribe;

  };
```

## deletePost
```jsx
  const deletePost = async (id) => {

    const docRef = doc(db, "posts", id); //may go on and on inside specifications

    await deleteDoc(docRef);

  };
```
