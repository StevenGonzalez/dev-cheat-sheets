# React Native Cheat Sheet

Quick reference for React Native mobile app development. React Native enables building native mobile apps using React and JavaScript/TypeScript for iOS and Android.

## Table of Contents

- [Setup and Installation](#setup-and-installation)
- [Project Structure](#project-structure)
- [Core Components](#core-components)
- [Hooks and State](#hooks-and-state)
- [Navigation](#navigation)
- [Styling](#styling)
- [Layout with Flexbox](#layout-with-flexbox)
- [Platform-Specific Code](#platform-specific-code)
- [Handling User Input](#handling-user-input)
- [Lists and Data](#lists-and-data)
- [Networking](#networking)
- [Storage](#storage)
- [Device APIs](#device-apis)
- [Performance Optimization](#performance-optimization)
- [Testing](#testing)
- [Building and Deployment](#building-and-deployment)
- [Debugging](#debugging)
- [Best Practices](#best-practices)
- [Common Patterns](#common-patterns)
- [Tools & Resources](#tools--resources)

## Setup and Installation

```bash
# Install React Native CLI (2026 recommended approach)
npm install -g @react-native-community/cli

# Create new project
npx @react-native-community/cli@latest init MyApp

# Create with TypeScript
npx @react-native-community/cli@latest init MyApp --template react-native-template-typescript

# Using Expo (managed workflow)
npx create-expo-app MyApp
cd MyApp
npx expo start

# Install dependencies
npm install
# or
yarn install

# Run on iOS (requires Xcode)
npx react-native run-ios

# Run on Android (requires Android Studio)
npx react-native run-android

# Metro bundler
npx react-native start
```

## Project Structure

```
MyApp/
├── android/                 # Android-specific code
├── ios/                     # iOS-specific code
├── src/
│   ├── components/          # Reusable components
│   ├── screens/            # Screen components
│   ├── navigation/         # Navigation configuration
│   ├── hooks/              # Custom hooks
│   ├── services/           # API services
│   ├── utils/              # Utility functions
│   ├── types/              # TypeScript type definitions
│   └── styles/             # Shared styles
├── __tests__/              # Test files
├── package.json
├── metro.config.js         # Metro bundler configuration
├── babel.config.js         # Babel configuration
└── App.tsx                 # Root component
```

## Core Components

```tsx
import React from 'react';
import {
  View,
  Text,
  StyleSheet,
  ScrollView,
  TouchableOpacity,
  Image,
  TextInput,
  Alert,
  SafeAreaView,
  StatusBar,
} from 'react-native';

// Basic component structure
const MyComponent: React.FC = () => {
  return (
    <SafeAreaView style={styles.container}>
      <StatusBar barStyle="dark-content" backgroundColor="#ffffff" />
      
      {/* Text display */}
      <Text style={styles.title}>Hello World</Text>
      <Text style={styles.subtitle}>React Native App</Text>
      
      {/* Image */}
      <Image
        source={{ uri: 'https://example.com/image.jpg' }}
        style={styles.image}
        resizeMode="cover"
      />
      
      {/* Local image */}
      <Image source={require('./assets/logo.png')} style={styles.logo} />
      
      {/* Touchable button */}
      <TouchableOpacity style={styles.button} onPress={handlePress}>
        <Text style={styles.buttonText}>Press Me</Text>
      </TouchableOpacity>
      
      {/* Text input */}
      <TextInput
        style={styles.input}
        placeholder="Enter text"
        value={text}
        onChangeText={setText}
        autoCapitalize="none"
        keyboardType="email-address"
      />
      
      {/* Scrollable content */}
      <ScrollView style={styles.scrollView}>
        {/* Content that can scroll */}
      </ScrollView>
    </SafeAreaView>
  );
};

const handlePress = () => {
  Alert.alert('Button Pressed', 'You pressed the button!');
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#ffffff',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    textAlign: 'center',
    marginVertical: 20,
  },
  subtitle: {
    fontSize: 16,
    textAlign: 'center',
    color: '#666',
  },
  image: {
    width: 200,
    height: 200,
    alignSelf: 'center',
    marginVertical: 20,
  },
  logo: {
    width: 100,
    height: 100,
    alignSelf: 'center',
  },
  button: {
    backgroundColor: '#007AFF',
    padding: 15,
    borderRadius: 8,
    margin: 20,
  },
  buttonText: {
    color: 'white',
    textAlign: 'center',
    fontSize: 16,
    fontWeight: '600',
  },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 8,
    padding: 12,
    margin: 20,
    fontSize: 16,
  },
  scrollView: {
    flex: 1,
  },
});
```

## Hooks and State

```tsx
import React, { useState, useEffect, useCallback, useMemo } from 'react';
import { View, Text, Button } from 'react-native';

// State management with hooks
const CounterComponent: React.FC = () => {
  // useState for local state
  const [count, setCount] = useState(0);
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(false);

  // useEffect for side effects
  useEffect(() => {
    // Component mount
    console.log('Component mounted');
    
    // Cleanup function
    return () => {
      console.log('Component unmounted');
    };
  }, []);

  useEffect(() => {
    // Effect with dependencies
    if (count > 10) {
      Alert.alert('High Count', 'Count exceeded 10!');
    }
  }, [count]);

  // useCallback to memoize functions
  const increment = useCallback(() => {
    setCount(prev => prev + 1);
  }, []);

  const decrement = useCallback(() => {
    setCount(prev => Math.max(0, prev - 1));
  }, []);

  // useMemo for expensive calculations
  const expensiveValue = useMemo(() => {
    return count * count * Math.random();
  }, [count]);

  // Custom hook example
  const { data, loading: dataLoading, error } = useApi('/api/data');

  return (
    <View style={{ padding: 20 }}>
      <Text>Count: {count}</Text>
      <Text>Expensive Value: {expensiveValue.toFixed(2)}</Text>
      <Button title="+" onPress={increment} />
      <Button title="-" onPress={decrement} />
      
      {dataLoading && <Text>Loading...</Text>}
      {error && <Text>Error: {error}</Text>}
      {data && <Text>Data loaded successfully</Text>}
    </View>
  );
};

// Custom hook
function useApi(url: string) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        const response = await fetch(url);
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err instanceof Error ? err.message : 'Unknown error');
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return { data, loading, error };
}

// Context for global state
const ThemeContext = React.createContext({
  theme: 'light',
  toggleTheme: () => {},
});

export const useTheme = () => {
  const context = React.useContext(ThemeContext);
  if (!context) {
    throw new Error('useTheme must be used within ThemeProvider');
  }
  return context;
};
```

## Navigation

```tsx
// Install: npm install @react-navigation/native @react-navigation/native-stack
// For React Navigation 6+

import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import { createDrawerNavigator } from '@react-navigation/drawer';

// Type definitions
export type RootStackParamList = {
  Home: undefined;
  Profile: { userId: string };
  Settings: undefined;
};

const Stack = createNativeStackNavigator<RootStackParamList>();
const Tab = createBottomTabNavigator();
const Drawer = createDrawerNavigator();

// Stack Navigator
function AppNavigator() {
  return (
    <NavigationContainer>
      <Stack.Navigator
        initialRouteName="Home"
        screenOptions={{
          headerStyle: { backgroundColor: '#007AFF' },
          headerTintColor: 'white',
          headerTitleStyle: { fontWeight: 'bold' },
        }}
      >
        <Stack.Screen 
          name="Home" 
          component={HomeScreen}
          options={{ title: 'My App' }}
        />
        <Stack.Screen 
          name="Profile" 
          component={ProfileScreen}
          options={({ route }) => ({ 
            title: `Profile ${route.params.userId}` 
          })}
        />
        <Stack.Screen name="Settings" component={SettingsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

// Tab Navigator
function TabNavigator() {
  return (
    <Tab.Navigator
      screenOptions={({ route }) => ({
        tabBarIcon: ({ focused, color, size }) => {
          let iconName = route.name === 'Home' ? 'home' : 'settings';
          return <Icon name={iconName} size={size} color={color} />;
        },
        tabBarActiveTintColor: '#007AFF',
        tabBarInactiveTintColor: 'gray',
      })}
    >
      <Tab.Screen name="Home" component={HomeScreen} />
      <Tab.Screen name="Settings" component={SettingsScreen} />
    </Tab.Navigator>
  );
}

// Screen components with navigation
import { NativeStackNavigationProp } from '@react-navigation/native-stack';
import { RouteProp } from '@react-navigation/native';

type HomeScreenProps = {
  navigation: NativeStackNavigationProp<RootStackParamList, 'Home'>;
};

const HomeScreen: React.FC<HomeScreenProps> = ({ navigation }) => {
  const goToProfile = () => {
    navigation.navigate('Profile', { userId: '123' });
  };

  const goToSettings = () => {
    navigation.navigate('Settings');
  };

  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <Text>Home Screen</Text>
      <Button title="Go to Profile" onPress={goToProfile} />
      <Button title="Go to Settings" onPress={goToSettings} />
    </View>
  );
};

type ProfileScreenProps = {
  route: RouteProp<RootStackParamList, 'Profile'>;
  navigation: NativeStackNavigationProp<RootStackParamList, 'Profile'>;
};

const ProfileScreen: React.FC<ProfileScreenProps> = ({ route, navigation }) => {
  const { userId } = route.params;

  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <Text>Profile Screen for User: {userId}</Text>
      <Button title="Go Back" onPress={() => navigation.goBack()} />
    </View>
  );
};

// Navigation options
const screenOptions = {
  headerShown: false,
  gestureEnabled: true,
  animationTypeForReplace: 'push' as const,
};
```

## Styling

```tsx
import { StyleSheet, Dimensions } from 'react-native';

const { width, height } = Dimensions.get('window');

// StyleSheet creation
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#ffffff',
    paddingHorizontal: 20,
  },
  
  // Typography
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#333',
    textAlign: 'center',
    marginBottom: 20,
  },
  
  subtitle: {
    fontSize: 16,
    color: '#666',
    lineHeight: 24,
  },
  
  // Layout
  row: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'space-between',
  },
  
  column: {
    flexDirection: 'column',
  },
  
  centered: {
    justifyContent: 'center',
    alignItems: 'center',
  },
  
  // Cards and containers
  card: {
    backgroundColor: 'white',
    borderRadius: 12,
    padding: 16,
    marginVertical: 8,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 3, // Android shadow
  },
  
  // Buttons
  primaryButton: {
    backgroundColor: '#007AFF',
    paddingVertical: 12,
    paddingHorizontal: 24,
    borderRadius: 8,
    alignItems: 'center',
  },
  
  secondaryButton: {
    backgroundColor: 'transparent',
    borderWidth: 1,
    borderColor: '#007AFF',
    paddingVertical: 12,
    paddingHorizontal: 24,
    borderRadius: 8,
    alignItems: 'center',
  },
  
  buttonText: {
    color: 'white',
    fontSize: 16,
    fontWeight: '600',
  },
  
  // Input styles
  input: {
    borderWidth: 1,
    borderColor: '#ddd',
    borderRadius: 8,
    padding: 12,
    fontSize: 16,
    backgroundColor: 'white',
  },
  
  inputError: {
    borderColor: '#ff3333',
  },
  
  // Responsive design
  responsive: {
    width: width > 400 ? '80%' : '95%',
    alignSelf: 'center',
  },
});

// Dynamic styles
const createStyles = (theme: 'light' | 'dark') => StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: theme === 'light' ? '#ffffff' : '#1a1a1a',
  },
  text: {
    color: theme === 'light' ? '#333333' : '#ffffff',
  },
});

// Platform-specific styles
const platformStyles = StyleSheet.create({
  container: {
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.1,
        shadowRadius: 4,
      },
      android: {
        elevation: 4,
      },
    }),
  },
});

// Style composition
const combinedStyles = StyleSheet.create({
  button: {
    ...styles.primaryButton,
    ...platformStyles.container,
  },
});
```

## Layout with Flexbox

```tsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const FlexboxExample: React.FC = () => {
  return (
    <View style={styles.container}>
      {/* Basic flex layout */}
      <View style={styles.flexRow}>
        <View style={styles.box}>
          <Text>1</Text>
        </View>
        <View style={styles.box}>
          <Text>2</Text>
        </View>
        <View style={styles.box}>
          <Text>3</Text>
        </View>
      </View>

      {/* Flexible items */}
      <View style={styles.flexContainer}>
        <View style={[styles.flexItem, { flex: 1 }]}>
          <Text>flex: 1</Text>
        </View>
        <View style={[styles.flexItem, { flex: 2 }]}>
          <Text>flex: 2</Text>
        </View>
        <View style={[styles.flexItem, { flex: 1 }]}>
          <Text>flex: 1</Text>
        </View>
      </View>

      {/* Alignment examples */}
      <View style={styles.alignmentContainer}>
        <View style={styles.centeredBox}>
          <Text>Centered</Text>
        </View>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
  
  // Flex direction
  flexRow: {
    flexDirection: 'row', // 'row' | 'column' | 'row-reverse' | 'column-reverse'
    height: 60,
    marginBottom: 20,
  },
  
  // Justify content (main axis)
  justifyStart: {
    justifyContent: 'flex-start', // Default
  },
  justifyCenter: {
    justifyContent: 'center',
  },
  justifyEnd: {
    justifyContent: 'flex-end',
  },
  justifySpaceBetween: {
    justifyContent: 'space-between',
  },
  justifySpaceAround: {
    justifyContent: 'space-around',
  },
  justifySpaceEvenly: {
    justifyContent: 'space-evenly',
  },
  
  // Align items (cross axis)
  alignStart: {
    alignItems: 'flex-start',
  },
  alignCenter: {
    alignItems: 'center',
  },
  alignEnd: {
    alignItems: 'flex-end',
  },
  alignStretch: {
    alignItems: 'stretch', // Default
  },
  
  // Complete centering
  centered: {
    justifyContent: 'center',
    alignItems: 'center',
  },
  
  // Flex wrap
  flexWrap: {
    flexWrap: 'wrap', // 'nowrap' | 'wrap' | 'wrap-reverse'
  },
  
  box: {
    width: 60,
    height: 60,
    backgroundColor: '#007AFF',
    margin: 5,
    justifyContent: 'center',
    alignItems: 'center',
  },
  
  flexContainer: {
    flexDirection: 'row',
    height: 60,
    marginBottom: 20,
  },
  
  flexItem: {
    backgroundColor: '#34C759',
    margin: 5,
    justifyContent: 'center',
    alignItems: 'center',
  },
  
  alignmentContainer: {
    height: 100,
    backgroundColor: '#F2F2F7',
    justifyContent: 'center',
    alignItems: 'center',
  },
  
  centeredBox: {
    width: 80,
    height: 40,
    backgroundColor: '#FF3B30',
    justifyContent: 'center',
    alignItems: 'center',
  },
});

// Position examples
const positionStyles = StyleSheet.create({
  relative: {
    position: 'relative', // Default
  },
  absolute: {
    position: 'absolute',
    top: 10,
    left: 10,
    right: 10,
    bottom: 10,
  },
  absoluteCentered: {
    position: 'absolute',
    top: '50%',
    left: '50%',
    transform: [{ translateX: -50 }, { translateY: -50 }],
  },
});
```

## Platform-Specific Code

```tsx
import { Platform, StatusBar } from 'react-native';

// Platform detection
const MyComponent: React.FC = () => {
  const isIOS = Platform.OS === 'ios';
  const isAndroid = Platform.OS === 'android';
  
  return (
    <View style={styles.container}>
      <Text>Platform: {Platform.OS}</Text>
      <Text>Version: {Platform.Version}</Text>
      
      {isIOS && (
        <Text>iOS specific content</Text>
      )}
      
      {isAndroid && (
        <Text>Android specific content</Text>
      )}
    </View>
  );
};

// Platform.select for styles
const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: Platform.select({
      ios: 44, // iOS status bar height
      android: StatusBar.currentHeight || 24,
    }),
  },
  
  text: {
    ...Platform.select({
      ios: {
        fontFamily: 'System',
        fontSize: 17,
      },
      android: {
        fontFamily: 'Roboto',
        fontSize: 16,
      },
    }),
  },
  
  shadow: {
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.25,
        shadowRadius: 3.84,
      },
      android: {
        elevation: 5,
      },
    }),
  },
});

// Platform-specific file imports
// File: Button.ios.tsx
export const PlatformButton: React.FC = () => (
  <TouchableOpacity>
    <Text>iOS Button</Text>
  </TouchableOpacity>
);

// File: Button.android.tsx
export const PlatformButton: React.FC = () => (
  <TouchableNativeFeedback>
    <View>
      <Text>Android Button</Text>
    </View>
  </TouchableNativeFeedback>
);

// Usage (React Native will automatically pick the right file)
import { PlatformButton } from './Button';
```

## Handling User Input

```tsx
import React, { useState } from 'react';
import {
  View,
  Text,
  TextInput,
  TouchableOpacity,
  Switch,
  Slider,
  Alert,
  Keyboard,
  KeyboardAvoidingView,
  Platform,
} from 'react-native';

const InputExample: React.FC = () => {
  const [text, setText] = useState('');
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [isEnabled, setIsEnabled] = useState(false);
  const [sliderValue, setSliderValue] = useState(50);

  const handleSubmit = () => {
    Keyboard.dismiss();
    Alert.alert('Form Submitted', `Text: ${text}, Email: ${email}`);
  };

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      {/* Basic text input */}
      <TextInput
        style={styles.input}
        placeholder="Enter text"
        value={text}
        onChangeText={setText}
        autoCapitalize="words"
        autoCorrect={true}
      />

      {/* Email input */}
      <TextInput
        style={styles.input}
        placeholder="Email address"
        value={email}
        onChangeText={setEmail}
        keyboardType="email-address"
        autoCapitalize="none"
        autoComplete="email"
        textContentType="emailAddress"
      />

      {/* Password input */}
      <TextInput
        style={styles.input}
        placeholder="Password"
        value={password}
        onChangeText={setPassword}
        secureTextEntry={true}
        autoCapitalize="none"
        textContentType="password"
      />

      {/* Multiline text input */}
      <TextInput
        style={[styles.input, styles.multilineInput]}
        placeholder="Enter description"
        multiline={true}
        numberOfLines={4}
        textAlignVertical="top"
      />

      {/* Switch toggle */}
      <View style={styles.switchContainer}>
        <Text>Enable notifications</Text>
        <Switch
          trackColor={{ false: '#767577', true: '#81b0ff' }}
          thumbColor={isEnabled ? '#f5dd4b' : '#f4f3f4'}
          onValueChange={setIsEnabled}
          value={isEnabled}
        />
      </View>

      {/* Slider */}
      <View style={styles.sliderContainer}>
        <Text>Volume: {Math.round(sliderValue)}%</Text>
        <Slider
          style={styles.slider}
          minimumValue={0}
          maximumValue={100}
          value={sliderValue}
          onValueChange={setSliderValue}
          minimumTrackTintColor="#1fb28a"
          maximumTrackTintColor="#d3d3d3"
          thumbStyle={{ backgroundColor: '#1fb28a' }}
        />
      </View>

      {/* Submit button */}
      <TouchableOpacity style={styles.button} onPress={handleSubmit}>
        <Text style={styles.buttonText}>Submit</Text>
      </TouchableOpacity>
    </KeyboardAvoidingView>
  );
};

const inputStyles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
  input: {
    borderWidth: 1,
    borderColor: '#ddd',
    borderRadius: 8,
    padding: 12,
    marginBottom: 16,
    fontSize: 16,
    backgroundColor: 'white',
  },
  multilineInput: {
    height: 100,
  },
  switchContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginBottom: 16,
  },
  sliderContainer: {
    marginBottom: 20,
  },
  slider: {
    width: '100%',
    height: 40,
  },
  button: {
    backgroundColor: '#007AFF',
    padding: 15,
    borderRadius: 8,
    alignItems: 'center',
  },
  buttonText: {
    color: 'white',
    fontSize: 16,
    fontWeight: 'bold',
  },
});
```

## Lists and Data

```tsx
import React, { useState, useEffect } from 'react';
import {
  FlatList,
  SectionList,
  VirtualizedList,
  Text,
  View,
  TouchableOpacity,
  Image,
  RefreshControl,
  ActivityIndicator,
} from 'react-native';

// Types
interface User {
  id: string;
  name: string;
  email: string;
  avatar: string;
}

interface Section {
  title: string;
  data: User[];
}

// FlatList example
const UserList: React.FC = () => {
  const [users, setUsers] = useState<User[]>([]);
  const [loading, setLoading] = useState(true);
  const [refreshing, setRefreshing] = useState(false);
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);

  useEffect(() => {
    loadUsers();
  }, []);

  const loadUsers = async () => {
    try {
      const response = await fetch(`/api/users?page=${page}`);
      const newUsers = await response.json();
      
      if (page === 1) {
        setUsers(newUsers);
      } else {
        setUsers(prev => [...prev, ...newUsers]);
      }
      
      setHasMore(newUsers.length > 0);
    } catch (error) {
      console.error('Error loading users:', error);
    } finally {
      setLoading(false);
      setRefreshing(false);
    }
  };

  const onRefresh = () => {
    setRefreshing(true);
    setPage(1);
    loadUsers();
  };

  const loadMore = () => {
    if (hasMore && !loading) {
      setPage(prev => prev + 1);
      loadUsers();
    }
  };

  const renderUser = ({ item }: { item: User }) => (
    <TouchableOpacity style={styles.userItem}>
      <Image source={{ uri: item.avatar }} style={styles.avatar} />
      <View style={styles.userInfo}>
        <Text style={styles.userName}>{item.name}</Text>
        <Text style={styles.userEmail}>{item.email}</Text>
      </View>
    </TouchableOpacity>
  );

  const renderFooter = () => {
    if (!loading) return null;
    return <ActivityIndicator size="large" color="#007AFF" />;
  };

  const keyExtractor = (item: User) => item.id;

  return (
    <FlatList
      data={users}
      renderItem={renderUser}
      keyExtractor={keyExtractor}
      refreshControl={
        <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
      }
      onEndReached={loadMore}
      onEndReachedThreshold={0.1}
      ListFooterComponent={renderFooter}
      ItemSeparatorComponent={() => <View style={styles.separator} />}
      contentContainerStyle={styles.listContainer}
      showsVerticalScrollIndicator={false}
    />
  );
};

// SectionList example
const GroupedUserList: React.FC = () => {
  const [sections, setSections] = useState<Section[]>([]);

  const renderSectionHeader = ({ section }: { section: Section }) => (
    <View style={styles.sectionHeader}>
      <Text style={styles.sectionTitle}>{section.title}</Text>
    </View>
  );

  return (
    <SectionList
      sections={sections}
      renderItem={renderUser}
      renderSectionHeader={renderSectionHeader}
      keyExtractor={keyExtractor}
      stickySectionHeadersEnabled={true}
      contentContainerStyle={styles.listContainer}
    />
  );
};

const listStyles = StyleSheet.create({
  listContainer: {
    padding: 16,
  },
  userItem: {
    flexDirection: 'row',
    padding: 16,
    backgroundColor: 'white',
    borderRadius: 8,
    marginBottom: 8,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 1 },
    shadowOpacity: 0.2,
    shadowRadius: 2,
    elevation: 2,
  },
  avatar: {
    width: 50,
    height: 50,
    borderRadius: 25,
    marginRight: 16,
  },
  userInfo: {
    flex: 1,
    justifyContent: 'center',
  },
  userName: {
    fontSize: 16,
    fontWeight: 'bold',
    marginBottom: 4,
  },
  userEmail: {
    fontSize: 14,
    color: '#666',
  },
  separator: {
    height: 1,
    backgroundColor: '#eee',
  },
  sectionHeader: {
    backgroundColor: '#f0f0f0',
    padding: 8,
    borderRadius: 4,
    marginBottom: 8,
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#333',
  },
});
```

## Networking

```tsx
import React, { useState, useEffect } from 'react';

// Fetch API
const useApiData = (url: string) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        const response = await fetch(url, {
          method: 'GET',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer token_here',
          },
        });

        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }

        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err instanceof Error ? err.message : 'Unknown error');
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return { data, loading, error };
};

// POST request
const createUser = async (userData: any) => {
  try {
    const response = await fetch('/api/users', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(userData),
    });

    if (!response.ok) {
      throw new Error('Failed to create user');
    }

    return await response.json();
  } catch (error) {
    console.error('Error creating user:', error);
    throw error;
  }
};

// Upload file
const uploadImage = async (imageUri: string) => {
  const formData = new FormData();
  formData.append('image', {
    uri: imageUri,
    type: 'image/jpeg',
    name: 'image.jpg',
  } as any);

  try {
    const response = await fetch('/api/upload', {
      method: 'POST',
      headers: {
        'Content-Type': 'multipart/form-data',
      },
      body: formData,
    });

    return await response.json();
  } catch (error) {
    console.error('Upload error:', error);
    throw error;
  }
};

// Network state monitoring
import NetInfo from '@react-native-async-storage/async-storage';

const NetworkStatus: React.FC = () => {
  const [isConnected, setIsConnected] = useState<boolean | null>(null);

  useEffect(() => {
    const unsubscribe = NetInfo.addEventListener(state => {
      setIsConnected(state.isConnected);
    });

    return unsubscribe;
  }, []);

  return (
    <View>
      <Text>
        Network Status: {isConnected ? 'Connected' : 'Disconnected'}
      </Text>
    </View>
  );
};
```

## Storage

```tsx
// AsyncStorage
import AsyncStorage from '@react-native-async-storage/async-storage';

// Store data
const storeData = async (key: string, value: string) => {
  try {
    await AsyncStorage.setItem(key, value);
  } catch (error) {
    console.error('Error storing data:', error);
  }
};

// Store object
const storeObject = async (key: string, value: any) => {
  try {
    const jsonValue = JSON.stringify(value);
    await AsyncStorage.setItem(key, jsonValue);
  } catch (error) {
    console.error('Error storing object:', error);
  }
};

// Retrieve data
const getData = async (key: string) => {
  try {
    const value = await AsyncStorage.getItem(key);
    return value !== null ? value : null;
  } catch (error) {
    console.error('Error retrieving data:', error);
  }
};

// Retrieve object
const getObject = async (key: string) => {
  try {
    const jsonValue = await AsyncStorage.getItem(key);
    return jsonValue != null ? JSON.parse(jsonValue) : null;
  } catch (error) {
    console.error('Error retrieving object:', error);
  }
};

// Remove data
const removeData = async (key: string) => {
  try {
    await AsyncStorage.removeItem(key);
  } catch (error) {
    console.error('Error removing data:', error);
  }
};

// Clear all data
const clearAll = async () => {
  try {
    await AsyncStorage.clear();
  } catch (error) {
    console.error('Error clearing storage:', error);
  }
};

// Custom storage hook
const useAsyncStorage = (key: string, initialValue: any) => {
  const [value, setValue] = useState(initialValue);

  useEffect(() => {
    const loadValue = async () => {
      const storedValue = await getObject(key);
      if (storedValue !== null) {
        setValue(storedValue);
      }
    };
    loadValue();
  }, [key]);

  const updateValue = async (newValue: any) => {
    setValue(newValue);
    await storeObject(key, newValue);
  };

  return [value, updateValue];
};
```

## Device APIs

```tsx
import { Alert, Linking, Vibration, Share } from 'react-native';
import { Camera } from 'expo-camera';
import * as Location from 'expo-location';
import * as Contacts from 'expo-contacts';

// Camera access
const CameraExample: React.FC = () => {
  const [hasPermission, setHasPermission] = useState<boolean | null>(null);

  useEffect(() => {
    (async () => {
      const { status } = await Camera.requestCameraPermissionsAsync();
      setHasPermission(status === 'granted');
    })();
  }, []);

  const takePicture = async () => {
    if (hasPermission) {
      // Camera logic here
    }
  };

  return (
    <View>
      {hasPermission && (
        <TouchableOpacity onPress={takePicture}>
          <Text>Take Picture</Text>
        </TouchableOpacity>
      )}
    </View>
  );
};

// Location services
const LocationExample: React.FC = () => {
  const [location, setLocation] = useState<Location.LocationObject | null>(null);

  useEffect(() => {
    (async () => {
      let { status } = await Location.requestForegroundPermissionsAsync();
      if (status !== 'granted') {
        Alert.alert('Permission denied', 'Location permission required');
        return;
      }

      let currentLocation = await Location.getCurrentPositionAsync({});
      setLocation(currentLocation);
    })();
  }, []);

  return (
    <View>
      {location && (
        <Text>
          Location: {location.coords.latitude}, {location.coords.longitude}
        </Text>
      )}
    </View>
  );
};

// Share content
const shareContent = async () => {
  try {
    await Share.share({
      message: 'Check out this awesome app!',
      url: 'https://example.com',
      title: 'My App',
    });
  } catch (error) {
    Alert.alert('Error', 'Failed to share content');
  }
};

// Open URL
const openURL = async (url: string) => {
  const supported = await Linking.canOpenURL(url);
  if (supported) {
    await Linking.openURL(url);
  } else {
    Alert.alert('Error', `Cannot open URL: ${url}`);
  }
};

// Vibration
const vibrate = () => {
  Vibration.vibrate(); // Default vibration
  // Vibration.vibrate([0, 500, 200, 500]); // Pattern: wait, vibrate, wait, vibrate
};
```

## Best Practices

```tsx
// 1. Use TypeScript
interface Props {
  title: string;
  onPress: () => void;
  disabled?: boolean;
}

const CustomButton: React.FC<Props> = ({ title, onPress, disabled = false }) => (
  <TouchableOpacity
    style={[styles.button, disabled && styles.buttonDisabled]}
    onPress={onPress}
    disabled={disabled}
  >
    <Text style={styles.buttonText}>{title}</Text>
  </TouchableOpacity>
);

// 2. Optimize FlatList performance
const OptimizedList: React.FC = () => (
  <FlatList
    data={data}
    renderItem={renderItem}
    keyExtractor={item => item.id}
    getItemLayout={(data, index) => ({
      length: ITEM_HEIGHT,
      offset: ITEM_HEIGHT * index,
      index,
    })} // If items have fixed height
    removeClippedSubviews={true}
    maxToRenderPerBatch={10}
    windowSize={10}
    initialNumToRender={10}
  />
);

// 3. Use React.memo for expensive components
const ExpensiveComponent = React.memo<Props>(({ data }) => {
  const processedData = useMemo(() => {
    return data.map(item => ({ ...item, processed: true }));
  }, [data]);

  return <View>{/* Render processed data */}</View>;
});

// 4. Error boundaries
class ErrorBoundary extends React.Component {
  constructor(props: any) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error: any) {
    return { hasError: true };
  }

  componentDidCatch(error: any, errorInfo: any) {
    console.error('Error caught by boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <Text>Something went wrong.</Text>;
    }

    return this.props.children;
  }
}

// 5. Safe area handling
import { useSafeAreaInsets } from 'react-native-safe-area-context';

const SafeScreen: React.FC = () => {
  const insets = useSafeAreaInsets();
  
  return (
    <View style={[styles.container, { paddingTop: insets.top }]}>
      {/* Content */}
    </View>
  );
};
```

## Tools & Resources

### Development Tools
- **Expo CLI**: Rapid development and testing
- **Flipper**: Advanced debugging platform
- **React Native Debugger**: Chrome-based debugger
- **Metro**: JavaScript bundler
- **Hermes**: JavaScript engine (Android)

### State Management
- **Redux Toolkit**: Modern Redux patterns
- **Zustand**: Lightweight state management
- **React Query**: Server state management
- **Context API**: Built-in React state

### UI Libraries
- **React Native Elements**: Cross-platform UI toolkit
- **NativeBase**: Mobile-first component library
- **Shoutem UI**: Customizable UI components
- **React Native Paper**: Material Design components

### Navigation
- **React Navigation 6+**: Standard navigation solution
- **React Native Navigation**: Native navigation

### Testing
- **Jest**: JavaScript testing framework
- **React Native Testing Library**: Component testing
- **Detox**: End-to-end testing
- **Maestro**: Mobile UI testing

### Performance
- **Reactotron**: Development tool for debugging
- **Performance Monitor**: Built-in performance tracking
- **Why Did You Render**: Performance debugging

### Useful Commands

```bash
# Development
npx react-native start
npx react-native run-ios
npx react-native run-android
npx react-native log-android
npx react-native log-ios

# Bundle analysis
npx react-native bundle --dev false --entry-file index.js --platform android --bundle-output bundle.js

# Clean builds
cd android && ./gradlew clean && cd ..
cd ios && xcodebuild clean && cd ..

# Reset Metro cache
npx react-native start --reset-cache

# Generate APK
cd android && ./gradlew assembleRelease

# Flipper debugging
npx react-native doctor
```

---

*This React Native cheat sheet covers modern mobile development practices for 2026. Keep dependencies updated and follow platform-specific guidelines for optimal performance.*