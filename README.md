import React, { useEffect, useState } from 'react';
import { View, Text, FlatList, Image, StyleSheet } from 'react-native';
import firestore from '@react-native-firebase/firestore';

const HomeScreen = () => {
  const [quotes, setQuotes] = useState([]);

  useEffect(() => {
    const fetchQuotes = async () => {
      const snapshot = await firestore().collection('quotes').get();
      setQuotes(snapshot.docs.map(doc => doc.data()));
    };
    fetchQuotes();
  }, []);

  return (
    <View style={styles.container}>
      <FlatList
        data={quotes}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <View style={styles.card}>
            <Image source={{ uri: item.imageUrl }} style={styles.image} />
            <Text style={styles.text}>{item.text}</Text>
          </View>
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, backgroundColor: '#f5f5f5' },
  card: { marginBottom: 16, backgroundColor: '#fff', borderRadius: 8, overflow: 'hidden' },
  image: { width: '100%', height: 200 },
  text: { padding: 16, fontSize: 16, color: '#333' },
});

export default HomeScreen;# Islamic-Golpo
