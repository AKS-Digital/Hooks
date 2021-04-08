# useAsyncStorage

Ce hooks a besoin d'utiliser la bibliothèque AsyncStorage pour écrire et lire les données dans la mémoire du téléphone.

## Installation des dépendances

```zsh
npm install @react-native-async-storage/async-storage
```

## Code

```ts
import AsyncStorage from '@react-native-async-storage/async-storage';

export const useAsyncStorage = () => {
  const handleError = (e: any) => {
    throw new Error(`useAsyncStorage : ${e.message}`);
  };

  const read = async (key: string) => {
    try {
      const jsonValue = await AsyncStorage.getItem(key);
      if (jsonValue === null)
        throw new Error(`the key '${key}' doesn't exists`);
      return JSON.parse(jsonValue);
    } catch (e) {
      return handleError(e);
    }
  };

  const write = async (key: string, value: any) => {
    try {
      const jsonValue = JSON.stringify(value);
      await AsyncStorage.setItem(key, jsonValue);
      return value;
    } catch (e) {
      return handleError(e);
    }
  };

  const remove = async (key: string) => {
    try {
      await AsyncStorage.removeItem(key);
      return key;
    } catch (e) {
      return handleError(e);
    }
  };

  return { read, write, remove };
};
```
