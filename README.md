# IC-notes-projects-tips


# Links to great videos and learning content

- Rust best practices -> https://www.youtube.com/watch?v=36L33S_DYHY 
- Build rust dapps -> Community conversations | overview of building a dapp in Rust 
- How to pitch my project to VCs -> https://www.youtube.com/watch?v=hK8r-W8p1GY Ledger canister -> watch Internet Identity -> https://www.youtube.com/watch?v=vCyQb9IHNQY 
- Frontends on IC: https://www.youtube.com/watch?v=rjSDvTaEj3s 
- Hosting on IC: https://www.youtube.com/watch?v=JAQ1dkFvfPI 
- Motoko intro: https://www.youtube.com/watch?v=WUqMwqt7abQ 
- Motoko intro: https://www.youtube.com/watch?v=WVeovvm3znE 
- Motoko school: https://www.youtube.com/watch?v=A5IYLmqr6YU 
- Encrypted notes: https://www.youtube.com/watch?v=I14cU7OlhmE 
- Dapp: https://www.youtube.com/watch?v=fFaNLKAgoUU 
- NFTs on IC: https://www.youtube.com/watch?v=040fTKgF9BI 
- Intro to IC: https://www.youtube.com/watch?v=Mo5erUD-rqs 
- Key chain tech: https://www.youtube.com/watch?v=vUcDRFC09J0 
- IC3D NFT: https://www.youtube.com/watch?v=kz4DoIiptAg 
- carstenj imageUpload: https://www.youtube.com/watch?v=0O4M0W47KKA 
- HTTP cert: https://www.youtube.com/watch?v=dw6SvDfv1Yk 
- Deploy cans in TS: https://www.youtube.com/watch?v=Mh_FWH-rMI4 
- NFT standards on IC: https://www.youtube.com/watch?v=vgxwPtuH3Qg 
- Design proposal SNS: https://www.youtube.com/watch?v=6V8nQ053aB8 
- Defi -> https://www.youtube.com/watch?v=HftK4xnlSs0 
- Hackathon workshop -> https://www.youtube.com/watch?v=nfgf3oS9W6Q 
- Mint an NFT -> https://www.youtube.com/watch?v=VGLcBISCB3Y 
- Http certification -> https://www.youtube.com/watch?v=dw6SvDfv1Yk 
- Certified variables -> https://www.youtube.com/watch?v=3mZHEfICi_U Portal demo -> https://www.youtube.com/watch?v=ZeHF-Lzciq8

# Encrypted notes dapp

https://internetcomputer.org/samples/encrypted-notes/ How to persist your user notes between upgrades - see time 37:30 in video https://www.youtube.com/watch?v=I14cU7OlhmE for the encrypted notes dapp. You will see two methods that persist the notes using stable variables. The methods are given below. Note this is all done inside the shared actor ->

shared({ caller = initializer }) actor class() {...};

// Below, we implement the upgrade hooks for our canister. // See https://smartcontracts.org/docs/language-guide/upgrades.html

// The work required before a canister upgrade begins. // See [nextNoteId], [stable_notesByUser], [stable_users] system func preupgrade() { Debug.print("Starting pre-upgrade hook..."); stable_notesByUser := Iter.toArray(notesByUser.entries()); stable_users := UserStore.serializeAll(users); Debug.print("pre-upgrade finished."); };

// The work required after a canister upgrade ends. // See [nextNoteId], [stable_notesByUser], [stable_users] system func postupgrade() { Debug.print("Starting post-upgrade hook..."); notesByUser := Map.fromIter<PrincipalName, List.List>( stable_notesByUser.vals(), stable_notesByUser.size(), Text.equal, Text.hash);

   users := UserStore.deserialize(stable_users, stable_notesByUser.size());
   stable_notesByUser := [];
   Debug.print("post-upgrade finished.");
};

Note: that the dapp allows many devices to be connected for the same user but for stability and security only 1000 users are allowed to register.

The II is a actor that is part of this dapp but is used as an external actor to the shared actor herein.

When we want to do a try-catch type assertion with exception, do the following with “expect(... , .);”: var existingNotes = expect(notesByUser.get(principalName), "registered user (principal " # principalName # ") w/o allocated notes"); The caller of this function is set in the actor initialization and then used throughout the code as “caller” in methods as a parameter: // in the actor creation part on top of all the code shared({ caller = initializer }) actor class() {...};

//in the methods throughout the code we use caller public shared({ caller }) func update_note(encrypted_note: EncryptedNote): async () {...};

# Cool projects on ICP 

- Openchat 
- Dbox 
- Dmail 
- Entrepot 
- Canistergeek 
- CanLista - https://k7gat-daaaa-aaaae-qaahq-cai.raw.ic0.app/listing/nns-ledger-10244/ryjl3-tyaaa-aaaaa-aaaba-cai
- cubetopia - https://devpost.com/software/cubetopia - hackathon winner 
- ICdevs - https://icdevs.org/who_we_are.html -icdevs by austin Fatheree - CTO 
