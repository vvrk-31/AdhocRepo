import com.okta.sdk.authc.credentials.ClientCredentials;
import com.okta.sdk.authc.credentials.TokenClientCredentials;
import com.okta.sdk.authc.credentials.UsernamePasswordCredentials;
import com.okta.sdk.client.Client;
import com.okta.sdk.client.Clients;
import com.okta.sdk.http.HttpRequest;
import com.okta.sdk.http.HttpResponse;
import com.okta.sdk.http.HttpClients;
import com.okta.sdk.http.HttpException;

public class OktaHttpWithUsernamePasswordExample {
    public static void main(String[] args) {
        Client client = Clients.builder()
            .setOrgUrl("https://{yourOktaDomain}")
            .build();

        // Authenticate with client credentials (client_id and client_secret)
        ClientCredentials clientCredentials = new ClientCredentials("{clientId}", "{clientSecret}");
        client.authenticateClient(clientCredentials);

        // Authenticate with username and password
        UsernamePasswordCredentials userCredentials = UsernamePasswordCredentials.builder()
            .setUsername("{username}")
            .setPassword("{password}")
            .build();
        TokenClientCredentials tokenClientCredentials = client.getUserCredentials(userCredentials);

        HttpRequest request = HttpRequests.newGetRequest("{yourApiUrl}");

        try {
            HttpResponse response = HttpClients.newOktaHttpClient(tokenClientCredentials).execute(request);
            System.out.println("Response Status: " + response.getStatusCode());
            System.out.println("Response Body: " + response.getBody());
        } catch (HttpException e) {
            e.printStackTrace();
        }
    }
}

implementation 'com.okta.sdk:okta-sdk-api:3.16.0'
implementation 'com.okta.sdk:okta-sdk-httpclient:3.16.0'

# AdhocRepo
