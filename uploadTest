package testeSFTP;

import java.io.File;

import com.jcraft.jsch.Channel;
import com.jcraft.jsch.ChannelSftp;
import com.jcraft.jsch.JSch;
import com.jcraft.jsch.Session;
import com.jcraft.jsch.SftpException;

public class testeUpload {
 
    @SuppressWarnings("unused")
	public static void main(String[] args)  {
    	ChannelSftp channelSftp = null;
        Session session = null;
        Channel channel = null;
        String host = "10.0.0.1"; // SFTP Host Name or SFTP Host IP Address
        String port = "22"; // SFTP Port Number
        String user = "test"; // User Name
        String password = "passwd"; // Password
        String dest = "/home/test/uploadTeste"; // Source Directory on SFTP server
        int contador = 0;
        try {
            JSch jsch = new JSch();
            session = jsch.getSession(user, host, port);
            session.setPassword(password);
            java.util.Properties config = new java.util.Properties();
            config.put("StrictHostKeyChecking", "no");
            session.setConfig(config);
            session.connect(); // Create SFTP Session
            channel = session.openChannel("sftp"); // Open SFTP Channel
            channel.connect();
            channelSftp = (ChannelSftp) channel;
            
            //the loop is not really necessary
            loopInfinito: while (true) {
	            File source = new File("D:\\Java\\eclipse\\eclipse-workspace\\testeSFTP\\a");
	            File[] fList = source.listFiles();
	
	            for (File file : fList){           
	                if (file.isFile()){
	                	try {
		                    String filename = file.getAbsolutePath();
		                    channelSftp.put(filename, dest, ChannelSftp.OVERWRITE);
		                    contador++;
		                    System.out.println(file + " transferred to " + dest);
	                	} catch (SftpException e) {
	                		e.printStackTrace();
	                	}
	                }
	            }
	            System.out.println("Upload de " + contador + " arquivos realizados");
	            Thread.sleep(8000);
            }
        } catch (Exception ex) {
            ex.printStackTrace();
        } finally {
            if (channelSftp != null)
                channelSftp.disconnect();
            if (channel != null)
                channel.disconnect();
            if (session != null)
                session.disconnect();
        }
    }
}
