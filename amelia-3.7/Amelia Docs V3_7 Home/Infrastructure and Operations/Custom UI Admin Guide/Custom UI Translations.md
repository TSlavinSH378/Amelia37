-   [Update Translated Properties](#CustomUITranslations-UpdateTranslatedProperties)
-   [Default Translated Properties](#CustomUITranslations-DefaultTranslatedProperties)
Amelia's Custom UI includes a default set of translated bits of text that cannot be changed, for example, text for `login` in Spanish set to `Iniciar Sesión` and `logout` in Spanish is set to `Cerrar Sesión` by default. One or more of these properties can be set to a different value with the `customTranslation` property in the config.json file.
While translations of conversations display the language set for the Amelia domain, the languages used in the user interface are English (en), Spanish (es), Dutch (nl), German (de), Swedish (se), Japanese (ja), Norwegian (no), Danish (da), and French (fr).
# Update Translated Properties
To update a translated property, create a JSON array to specify the language and one or more translated properties to update. The JSON array is set as the value for the `customTranslation` property in the config.json file. For example, the default text for the `tooltip` property can be set to overwrite the Spanish copy.
Set a language to the Amelia domain selection page by changing the language property** **in the config.json file to the language locale prefix, for example, es for Spanish.
This feature is available in Custom UI 5.12.0 or greater
``` groovy
{
    "language": "es"
}
```
To override a property in the translated properties file, update the `customTranslation` property in the config.json file under the ui property section.
``` groovy
"ui": {
    "customTranslation": {
        "en": {
            "tooltip": "My custom tooltip."
        },
        "es": {
            "tooltip": "Mi tooltip personalizado."
        }
    }
}
```
# Default Translated Properties
The Amelia Custom UI has a set of short text properties for a variety of languages. Properties are set in a single file. Property values are updated with the `customTranslation` property in the config.json file instead of the default file.
``` groovy
en: {
  cancelMessage: 'I changed my mind',
  hint: 'Type your message here...',
  login: 'Login',
  loginMessage: 'Login again',
  logout: 'Logout',
  feedback: 'Feedback',
  newConversation: 'Start new conversation',
  tooltip: 'Chat with our Virtual Assistant by typing your responses in the text box.',
  submit: 'Submit',
  resetConversation: 'Reset Conversation',
  seeChat: 'See Chat',
  useVoice: 'Use Voice',
  timeoutConvoEndMessage: 'Our session has ended. It was a pleasure chatting with you today!',
  changeDomain: 'Change Domain',
  agentHelp: 'Live Agent',
  escalationMessage: 'Escalating to live agent.',
  activeConversations: 'Active Conversations',
  privacyPolicy: 'Privacy Policy',
  mailTo: 'Contact Us',
  logoutConfirmation: {
    header: 'Progress will be lost',
    body: 'Continue logging out?',
    logoutButton: 'Leave Chat',
    closeModalButton: 'Resume'
  },
  agentHasJoinedMessage: 'Agent has joined',
  errorMessages: {
    fileExceedsLimit: 'The file exceeds 20MB: File is too big. Max file size: 20MB'
  },
  dragAndDrop: {
    dropFileHere: 'Drag & Drop file here',
    clickToUpload: 'or click to upload from computer',
    pressEnterToUpload: 'Press Enter to upload a file',
    tapToUpload: 'Tap to upload file'
  },
  selectDomainGreetings: {
    hi: 'Hi,',
    selectADomain: 'Select a domain',
    access: 'You have access to',
    toDomains: 'domains',
    search: 'Search'
  }
},
es: {
  hint: 'Escriba su mensaje aquí...',
  login: 'Iniciar Sesión',
  loginMessage: 'Ingresar de nuevo',
  logout: 'Cerrar Sesión',
  newConversation: 'Iniciar nueva conversación',
  tooltip: 'Amelia esta entrenada para realizar, restauración de contraseñas, solicitar la instalación de software y gestionar entornos. Describe lo que deseas realizar y Amelia hará lo mejor posible para ayudarte.',
  submit: 'Enviar',
  resetConversation: 'Restablecer Conversación',
  seeChat: 'Ver Chat',
  useVoice: 'Usar Voz',
  timeoutConvoEndMessage: 'Nuestra sesión ha terminado. ¡Fue un placer charlar contigo hoy!',
  changeDomain: 'Cambiar Idioma',
  agentHelp: 'Ayuda del Agente',
  activeConversations: 'Conversaciones Activas',
  agentHasJoinedMessage: 'Agente se ha unido',
  logoutConfirmation: {
    header: 'El progreso se perderá',
    body: 'Continuar saliendo?',
    logoutButton: 'Salir del chat',
    closeModalButton: 'Continuar'
  },
  feedback: 'Intimidad',
  errorMessages: {
    fileExceedsLimit: 'El archivo supera los 20 MB: el archivo es demasiado grande. Tamaño máximo de archivo: 20MB'
  },
  dragAndDrop: {
    dropFileHere: 'Arrastrar y soltar el archivo aquí',
    clickToUpload: 'o haga clic para subir desde la computadora',
    pressEnterToUpload: 'Presiona Enter para subir un archivo',
    tapToUpload: 'Toque para subir el archivo'
  },
  selectDomainGreetings: {
    hi: 'Hola,',
    selectADomain: 'Selecciona un dominio',
    access: 'Tienes acceso a',
    toDomains: 'dominios',
    search: 'Buscar'
  }
},
nl: {
  hint: 'Typ hier uw bericht...',
  login: 'Log in',
  loginMessage: 'Log opnieuw in',
  logout: 'Uitloggen',
  newConversation: 'Start een nieuw gesprek',
  tooltip: 'Chat met onze virtuele assistent door uw antwoorden in het tekstvak te typen',
  submit: 'Voorleggen',
  resetConversation: 'Conversatie opnieuw instellen',
  seeChat: 'Zie de Chat',
  useVoice: 'Gebruik Voice',
  timeoutConvoEndMessage: 'Onze sessie is beëindigd. Het was een genoegen chatten met u vandaag!',
  changeDomain: 'Taal Veranderen',
  agentHelp: 'Hulpvraag Medewerker',
  activeConversations: 'Actieve Gesprekken',
  agentHasJoinedMessage: 'Een medewerker neemt deel',
  logoutConfirmation: {
    header: 'Vooruitgang zal verloren gaan',
    body: 'Doorgaan met uitloggen?',
    logoutButton: 'Verlaat Chat',
    closeModalButton: 'Hervatten'
  },
  feedback: 'terugkoppeling',
  errorMessages: {
    fileExceedsLimit: 'Het bestand overschrijdt 20 MB: het bestand is te groot. Max bestandsgrootte: 20MB'
  },
  dragAndDrop: {
    dropFileHere: 'Drag & Drop bestand hier',
    clickToUpload: 'of klik om te uploaden vanaf de computer',
    pressEnterToUpload: 'Druk op Enter om een bestand te uploaden',
    tapToUpload: 'Tik om het bestand te uploaden'
  },
  selectDomainGreetings: {
    hi: 'Hallo,',
    selectADomain: 'Selecteer een domein',
    access: 'Je hebt toegang tot',
    toDomains: 'domeinen',
    search: 'Zoeken'
  }
},
de: {
  hint: 'Geben Sie Ihre Antwort hier ein',
  login: 'Anmelden',
  loginMessage: 'Nochmals einloggen',
  logout: 'Ausloggen',
  newConversation: 'Neue Unterhaltung beginnen',
  tooltip: 'Chatten Sie mit unserer virtuellen Assistentin, indem Sie Ihre Antworten hier eintippen',
  submit: 'Bestätigen',
  resetConversation: 'Unterhaltung neu starten',
  seeChat: 'Chatverlauf anzeigen',
  useVoice: 'Sprachsteuerung nutzen',
  timeoutConvoEndMessage: 'Unsere Unterhaltung ist beendet. Es hat mich gefreut, mit Ihnen zu chatten!',
  changeDomain: 'Sprache ändern',
  agentHelp: 'Mit Kundenberater chatten',
  activeConversations: 'Aktive Gespräche',
  agentHasJoinedMessage: 'Mitarbeiter im Chat',
  logoutConfirmation: {
    header: 'Der Fortschritt wird verloren gehen',
    body: 'Continue logging out?',
    logoutButton: 'Ausloggen?',
    closeModalButton: 'Fortsetzen'
  },
  feedback: 'Datenschutz',
  errorMessages: {
    fileExceedsLimit: 'Die Datei überschreitet 20 MB: Die Datei ist zu groß. Maximale Dateigröße: 20 MB'
  },
  dragAndDrop: {
    dropFileHere: 'Drag & Drop-Datei hier',
    clickToUpload: 'oder klicken Sie, um vom Computer hochzuladen',
    pressEnterToUpload: 'Drücken Sie die Eingabetaste, um eine Datei hochzuladen',
    tapToUpload: 'Tippen Sie hier, um die Datei hochzuladen'
  },
  selectDomainGreetings: {
    hi: 'Hallo',
    selectADomain: 'Bitte wählen Sie eine Domain',
    access: 'Sie haben Zugriff auf',
    toDomains: 'Domains',
    search: 'Suchen'
  }
},
sv: {
  hint: 'Skriv ditt meddelande här ...',
  login: 'Logga in',
  loginMessage: 'Logga in igen',
  logout: 'Logga ut',
  feedback: 'Feedback',
  newConversation: 'Starta ny konversation',
  tooltip: 'Chatta med vår virtuella assistent genom att skriva in dina svar i textrutan.',
  submit: 'Skicka',
  resetConversation: 'Återställ konversation',
  seeChat: 'Se chatt',
  useVoice: 'Använd Voice',
  timeoutConvoEndMessage: 'Vår session har slutat. Det var ett nöje att chatta med dig idag!',
  changeDomain: 'Ändra Domain',
  agentHelp: 'Ombud',
  escalationMessage: 'Eskalerar till ombud.',
  activeConversations: 'aktiva konversationer',
  privacyPolicy: 'Sekretesspolicy',
  mailTo: 'Kontakta oss',
  logoutConfirmation: {
    header: 'Progress kommer att gå förlorade',
    body: 'Fortsätt att logga ut?',
    logoutButton: 'Lämna chatt',
    closeModalButton: 'Återuppta'
  },
  agentHasJoinedMessage: 'En agent har tagit över',
  errorMessages: {
    fileExceedsLimit: 'Filen överstiger 20 MB: Filen är för stor. Max filstorlek: 20 MB'
  },
  dragAndDrop: {
    dropFileHere: 'Dra och släpp filen här',
    clickToUpload: 'eller klicka för att ladda upp från datorn',
    pressEnterToUpload: 'Tryck på Enter för att ladda upp en fil',
    tapToUpload: 'Tryck för att ladda upp filen'
  },
  selectDomainGreetings: {
    hi: 'Hej',
    selectADomain: 'Välj en domän',
    access: 'Du har tillgång till',
    toDomains: 'domäner',
    search: 'Sök'
  }
},
ja: {
  cancelMessage: '???????????',
  hint: '?????????????',
  login: '????',
  loginMessage: '?????????????',
  logout: '?????',
  feedback: '???????',
  newConversation: '?????????',
  tooltip: '?????????????????????????????',
  submit: '??',
  resetConversation: '???????',
  seeChat: '???????',
  useVoice: '????',
  timeoutConvoEndMessage: '????????????????????????????????',
  changeDomain: '??????',
  agentHelp: '????????',
  escalationMessage: '???????????????...',
  activeConversations: '??????',
  privacyPolicy: '??????????',
  mailTo: '??????',
  logoutConfirmation: {
    header: '??????????',
    body: '??????????????',
    logoutButton: '?????',
    closeModalButton: '????'
  },
  agentHasJoinedMessage: '??????????????',
  errorMessages: {
    fileExceedsLimit: '?????20MB???????????????????? ??????????20MB'
  },
  dragAndDrop: {
    dropFileHere: '?????????????????',
    clickToUpload: '??????????????????????',
    pressEnterToUpload: '???????????????Enter???????',
    tapToUpload: '??????????????????'
  },
  selectDomainGreetings: {
    hi: '?????',
    title: '?',
    selectADomain: '????????????',
    access: '????????????',
    toDomains: '??????',
    search: '??'
  }
},
no: {
  cancelMessage: 'Jeg har skiftet mening',
  hint: 'Skriv meldingen din her',
  login: 'Logg inn',
  loginMessage: 'Logg inn på nytt',
  logout: 'Logg ut',
  feedback: 'Tilbakemelding',
  newConversation: 'Start ny samtale',
  tooltip: 'Skriv i meldingsfeltet for å snakke med vår virtuelle assistent.',
  submit: 'Send',
  resetConversation: 'Start ny samtale',
  seeChat: 'Se samtale',
  useVoice: 'Bruk stemme',
  timeoutConvoEndMessage: 'Samtalen er avsluttet. Det var hyggelig å prate med deg!',
  changeDomain: 'Bytt domene',
  agentHelp: 'Menneskelig agent',
  escalationMessage: 'Overfører til en agent.',
  activeConversations: 'Aktive samtaler',
  privacyPolicy: 'Personvernserklæring',
  mailTo: 'Kontakt oss',
  logoutConfirmation: {
    header: 'Samtalen blir avbrutt',
    body: 'Vil du fortsette?',
    logoutButton: 'Forlat samtalen',
    closeModalButton: 'Gjenoppta samtalen'
  },
  agentHasJoinedMessage: 'Du snakker nå med en agent',
  errorMessages: {
    fileExceedsLimit: 'Filen overskrider 20 MB: Filen er for stor. Maks filstørrelse: 20 MB'
  },
  dragAndDrop: {
    dropFileHere: 'Dra & slipp fil her',
    clickToUpload: 'eller klikk for å laste opp fra datamaskinen',
    pressEnterToUpload: 'Trykk Enter for å laste opp en fil',
    tapToUpload: 'Trykk for å laste opp fil'
  },
  selectDomainGreetings: {
    hi: 'Hei',
    selectADomain: 'Velg et domene',
    access: 'Du har tilgang til',
    toDomains: 'domener',
    search: 'Søk'
  }
},
da: {
  cancelMessage: 'Jeg har ændret mening',
  hint: 'Skriv din besked her',
  login: 'Log ind',
  loginMessage: 'Log ind igen',
  logout: 'Log ud',
  feedback: 'Tilbagemelding',
  newConversation: 'Start ny samtale',
  tooltip: 'Skriv i meddelelsesboksen for at tale med vores virtuelle assistent.',
  submit: 'Send',
  resetConversation: 'Start en ny samtale',
  seeChat: 'Se samtale',
  useVoice: 'Brug stemme',
  timeoutConvoEndMessage: 'Samtalen er afsluttet. Det var en fornøjelse at prate med dig!',
  changeDomain: 'Skift domæne',
  agentHelp: 'Menneskelig agent',
  escalationMessage: 'Overfører til en agent.',
  activeConversations: 'Aktive samtaler',
  privacyPolicy: 'Persondataerklæring',
  mailTo: 'Kontakt os',
  logoutConfirmation: {
    header: 'Samtalen afbrydes',
    body: 'Vil du fortsætte?',
    logoutButton: 'Forlad samtale',
    closeModalButton: 'Genoptag samtale'
  },
  agentHasJoinedMessage: ' Du taler nu med en agent',
  errorMessages: {
    fileExceedsLimit: 'Filen overstiger 20 MB: Filen er for stor. Maks filstørrelse: 20MB'
  },
  dragAndDrop: {
    dropFileHere: 'Træk & slip fil her',
    clickToUpload: 'eller klik for at uploade fra computer',
    pressEnterToUpload: 'Tryk på Enter for at uploade en fil',
    tapToUpload: 'Tryk for at uploade filen'
  },
  selectDomainGreetings: {
    hi: 'Hej',
    selectADomain: 'Vælg et domæne',
    access: 'Du har adgang til',
    toDomains: 'domæner',
    search: 'Søg'
  }
},
fr: {
  cancelMessage: "J'ai changé d'avis",
  hint: 'Saisir votre message ici...',
  login: 'Connexion',
  loginMessage: 'Reconnexion',
  logout: 'Déconnexion',
  feedback: "Retour d'information",
  newConversation: 'Démarrer une nouvelle conversation',
  tooltip: 'Échanger avec notre agent virtuel en saisissant vos réponse dans le champ texte.',
  submit: 'Envoyer',
  resetConversation: 'Réinitialiser la conversation',
  seeChat: 'Observer la conversation',
  useVoice: 'Utiliser la voix',
  timeoutConvoEndMessage: 'La conversation est terminée. Ce fut un plaisir de discuter avec vous !',
  changeDomain: 'Changer de domaine',
  agentHelp: 'Agent humain',
  escalationMessage: 'Transférer vers un agent humain.',
  activeConversations: 'Conversations actives',
  privacyPolicy: 'Politique de confidentialité',
  mailTo: 'Nous contacter',
  logoutConfirmation: {
    header: 'Les informations seront perdues',
    body: 'Confirmer la déconnexion',
    logoutButton: 'Quitter la conversation',
    closeModalButton: 'Continuer'
  },
  agentHasJoinedMessage: 'Un agent a rejoint la discussion',
  errorMessages: {
    fileExceedsLimit: 'Le fichier dépasse 20 MB: le fichier est trop gros. Taille maximale du fichier: 20 MB'
  },
  dragAndDrop: {
    dropFileHere: 'Glisser-déposer le fichier ici',
    clickToUpload: "ou cliquez pour télécharger à partir de l'ordinateur",
    pressEnterToUpload: 'Appuyez sur Entrée pour télécharger un fichier.',
    tapToUpload: 'Appuyez sur pour télécharger le fichier'
  },
  selectDomainGreetings: {
    hi: 'Salut,',
    selectADomain: 'Sélectionnez un domaine',
    access: 'Vous avez accès à',
    toDomains: 'domaines',
    search: 'Chercher'
  }
}
```
