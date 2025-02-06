# Notes sur Next.js

Ces notes ont été prises par Ilias Benharrat au fur et à mesure de lundi et mardi et mercredi. Elles ont été rédigées en .md sur un IDE spécial pour le .md nommé StackEdit, ce qui explique l'absence de commits, car la prise de notes sur Visual Studio Code est compliquée et peu intuitive.

## Chapitre 1 : Introduction

Présentation de Next.js
- Next.js est un framework React qui permet de développer des applications web full-stack.
- Il offre des fonctionnalités avancées comme le rendu côté serveur, la génération de sites statiques, le streaming avec Suspense et la gestion d'API intégrée.
- Son principal avantage est d’optimiser les performances et le SEO grâce à un pré-rendu efficace.

## Chapitre 2 : Prise en Main

Installation
- Création d’un projet avec :
  ```sh
  npx create-next-app@latest my-app
  cd my-app
  npm run dev
  ```
- `npm run dev` lance l’application en mode développement sur `http://localhost:3000`.

Structure du Projet
- `app/` : Contient les pages et layouts de l’application.
- `public/` : Stocke les fichiers statiques (images, polices).
- `styles/` : Contient les fichiers CSS globaux.
- `next.config.js` : Fichier de configuration de Next.js.

## Chapitre 3 : Stylisation CSS

Options de Stylisation
Next.js permet plusieurs méthodes de stylisation :
- CSS Global : Styles appliqués à toute l’application (`app/global.css`).
- Modules CSS : Styles scopés à un composant (`component.module.css`).
- Tailwind CSS : Framework de classes utilitaires (`@tailwindcss`).
- Styled Components / Emotion : Approches CSS-in-JS.

Exemple avec Modules CSS :
```tsx
import styles from './button.module.css';

export default function Button() {
  return <button className={styles.primary}>Cliquez ici</button>;
}
```

## Chapitre 4 : Optimisation des Polices et Images

Gestion des Polices
- Optimisation automatique via `next/font`.
- Chargement au build pour éviter les requêtes externes.
- Exemple avec la police Inter :
  ```tsx
  import { Inter } from 'next/font/google';
  const inter = Inter({ subsets: ['latin'] });
  ```

Optimisation des Images avec `next/image`
- Chargement différé (lazy loading).
- Formats modernes (WebP, AVIF) gérés automatiquement.
- Exemple :
  ```tsx
  import Image from 'next/image';
  <Image src="/logo.png" width={200} height={100} alt="Logo" />
  ```

## Chapitre 5 : Création de Layouts et Pages

Layouts
- Permet de réutiliser une structure commune (ex: navbar, sidebar).
- Exemple d’un `layout.tsx` :
  ```tsx
  export default function Layout({ children }: { children: React.ReactNode }) {
    return (
      <div>
        <Navbar />
        {children}
      </div>
    );
  }
  ```

## Chapitre 6 : Navigation entre les Pages

Utilisation du composant `<Link>`
```tsx
import Link from 'next/link';
<Link href="/dashboard">Aller au Dashboard</Link>
```

Hook `useRouter()` pour la navigation dynamique
```tsx
import { useRouter } from 'next/navigation';
const router = useRouter();
router.push('/dashboard');
```

## Chapitre 7 : Configuration de la Base de Données

Connexion
- Utilisation de PostgreSQL ou MySQL via `@vercel/postgres`.
- Configuration dans `.env.local` :
  ```env
  DATABASE_URL=postgres://user:password@host:5432/database
  ```

Initialisation des Données
- Ajout d’un script de seeding :
  ```tsx
  await sql`INSERT INTO users (name) VALUES ('Alice')`;
  ```

## Chapitre 8 : Récupération des Données

Requêtes API et Base de Données
- Utilisation d’`async/await` dans un composant serveur :
  ```tsx
  export default async function Page() {
    const data = await fetch('https://api.example.com/products');
    return <div>{JSON.stringify(await data.json())}</div>;
  }
  ```

## Chapitre 9 : Rendu Statique et Dynamique

SSG (Static Site Generation)
- Pré-génération au build :
  ```tsx
  export async function generateStaticParams() {
    return [{ id: '1' }, { id: '2' }];
  }
  ```

SSR (Server-Side Rendering)
- Rendu dynamique à chaque requête :
  ```tsx
  export default async function Page() {
    const data = await fetch('https://api.example.com');
    return <div>{data}</div>;
  }
  ```
