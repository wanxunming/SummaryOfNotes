## React Native 学习笔记

### 1. `useQuery` (React Query 库)

#### useQuery的特性：

1. **自动数据缓存：** `useQuery` 会自动缓存从服务器获取的数据，避免不必要的重复请求，从而提高应用程序的性能。

2. **自动重新获取：** 如果数据发生变化或者查询条件变化，`useQuery` 会自动重新获取数据，并更新缓存。

3. **自动优化：** React Query 会智能地处理网络请求，避免过度渲染和不必要的请求。

4. **查询密钥（Query Key）：** `useQuery` 通过查询密钥来标识不同的数据查询。当查询密钥改变时，数据将被重新获取。

5. **数据同步：** 在多个组件中使用相同的查询密钥可以实现数据同步，确保所有组件都使用相同的数据。

6. **加载状态管理：** `useQuery` 提供了 `isLoading`、`isError`、`isSuccess` 等状态，用于管理数据加载过程中的状态。

7. **错误处理：** 你可以通过 `isError` 和 `error` 属性来处理请求过程中的错误。


#### useQuery的原理：

1. **数据缓存：** 当你使用 `useQuery` 进行数据请求时，React Query 会检查是否已经有缓存的数据。如果有，它会立即返回缓存数据，并在后台发起网络请求以获取最新数据。

2. **数据更新：** 在后台获取最新数据后，React Query 会更新缓存，并通过状态更新通知组件数据已更新。这可以避免因为数据更新而导致组件不必要的重新渲染。

3. **数据重新获取：** React Query 会周期性地重新获取数据，以确保数据的及时性。你可以设置重新获取的时间间隔。

4. **数据同步：** 通过使用相同的查询密钥，不同组件可以实现数据同步。当一个组件重新获取数据时，其他使用相同查询密钥的组件也会自动更新。


- ```jsx
  import { useQuery } from 'react-query';
  
  const fetchData = async () => {
    // 从 API 获取数据
  };
  
  const YourComponent = () => {
    const { data, isLoading, error } = useQuery('yourQueryKey', fetchData);
  
    if (isLoading) {
      return <p>Loading...</p>;
    }
  
    if (error) {
      return <p>Error: {error.message}</p>;
    }
  
    return <p>Data: {data}</p>;
  };
  ```



### 2. Context API

1. **创建 Context：** 使用 `React.createContext()` 创建一个 Context。这将返回一个对象，其中包含 `Provider` 和 `Consumer` 组件。
2. **Provider：** 使用 `Provider` 组件将状态数据提供给需要使用的子组件。`Provider` 接受一个 `value` 属性，该属性包含要共享的状态。
3. **Consumer：** 在需要访问共享状态的组件中，使用 `Consumer` 组件来消费状态。`Consumer` 接受一个函数作为子元素，并将当前共享状态传递给该函数。
4. **组件更新：** 当 `Provider` 中的状态发生变化时，所有使用该 `Context` 的 `Consumer` 组件都会重新渲染。这是由于 React 的重新渲染机制。
5. **性能优化：** React 使用了虚拟 DOM 和 diff 算法来优化组件的重新渲染，确保只有受影响的部分会重新渲染，从而减少性能开销。
6. **避免嵌套过深：** 虽然 Context API 可以避免 Props 层层传递，但过度使用 Context 可能会导致组件间关系复杂，不易维护。

- 创建上下文：
  ```jsx
  import React, { createContext, useContext, useState } from 'react';

  const MyContext = createContext();

  const MyProvider = ({ children }) => {
    const [data, setData] = useState('');

    return (
      <MyContext.Provider value={{ data, setData }}>
        {children}
      </MyContext.Provider>
    );
  };

  const ChildComponent = () => {
    const { data, setData } = useContext(MyContext);

    return (
      <div>
        <p>Data: {data}</p>
        <button onClick={() => setData('New Data')}>Update Data</button>
      </div>
    );
  };
  ```



### react-native-fs 多文件下载百分比

实现多文件下载并在界面上显示总体下载百分比需要更精细的控制。通过使用文件的大小来计算总体下载进度，并利用 `RNFS.downloadFile` 的 `progress` 回调来监测下载量，然后计算百分比。

```javascript
import RNFS from 'react-native-fs';
import React, { useState, useEffect } from 'react';

const YourComponent = () => {
  const filesToDownload = [
    { name: 'file1.txt', url: 'URL_OF_FILE1' },
    { name: 'file2.txt', url: 'URL_OF_FILE2' },
    // Add more files to download
  ];

  const [totalSize, setTotalSize] = useState(0);
  const [totalDownloaded, setTotalDownloaded] = useState(0);

  useEffect(() => {
    getTotalSize();
    downloadFiles();
  }, []);

  const getTotalSize = async () => {
    let total = 0;
    for (const file of filesToDownload) {
      try {
        const headers = await RNFS.head(file.url);
        total += parseInt(headers['Content-Length']);
      } catch (error) {
        console.log('Error getting file size:', error);
      }
    }
    setTotalSize(total);
  };

  const downloadFiles = async () => {
    const downloadPromises = filesToDownload.map((file) => {
      const downloadDest = RNFS.DocumentDirectoryPath + '/' + file.name;
      
      return RNFS.downloadFile({
        fromUrl: file.url,
        toFile: downloadDest,
        progressDivider: 1,
      }).promise.then((response) => {
        if (response.statusCode === 200) {
          setTotalDownloaded((prevTotal) => prevTotal + parseInt(response.bytesWritten));
        }
      });
    });

    try {
      await Promise.all(downloadPromises);
      console.log('All files downloaded successfully');
    } catch (error) {
      console.log('Error downloading files:', error);
    }
  };

  const downloadPercentage = (totalDownloaded / totalSize) * 100;

  return (
    <View>
      <Text>Total Downloaded: {downloadPercentage.toFixed(2)}%</Text>
    </View>
  );
};

export default YourComponent;
```

我们通过调用 `RNFS.head` 来获取每个文件的大小，并将所有文件的大小累加以获取总体下载文件大小。然后在下载文件时，我们利用 `RNFS.downloadFile` 的 `progress` 回调来监测下载量，并将下载的字节数累加以计算总体下载的字节数。最终，通过计算总体下载的百分比来显示下载进度。