import "@stdlib/ownable";
import "@stdlib/deploy";

import "./ft_base_program_user.tact";
import "./ft_user_storage.tact";
import "./ft_user_main.tact";

contract FtBaseProgramMain with Deployable, Ownable {
    const programName: String = "Base";
    const minTonsForStorage: Int = ton("0.04");
    
    gasMultiplier: Int as coins = ton("1.0");
    isSetup: Bool = false;

    owner: Address;
    master: Address;
    recipient: Address;
    levelPrices: map<Int as uint8, Int>;
    levelFees: map<Int as uint8, Int>;
    totalProfit: Int as coins = ton("0.0");

    init(master: Address){
        nativeThrowUnless(132, sender() == master);

        self.master = master;
        self.owner = sender();
        self.recipient = sender();

        self.setupLevelPrice();
        self.setupLevelFee();
    }

    receive(){}

    receive("PaymentForSquadCreation"){}

    receive("withdraw"){
        self.requireOwner();
        nativeReserve(self.minTonsForStorage, 0);

        send(SendParameters{
            to: self.recipient,
            value: 0,
            mode: SendRemainingBalance,
            body: "Your withdraw".asComment(),
        });
    }

    receive(msg: SetupBaseProgramMain){
        nativeThrowUnless(132, sender() == self.master);
        nativeThrowUnless(131, !self.isSetup);

        self.owner = msg.owner;
        self.recipient = msg.owner;
        self.isSetup = true;
        self.reply(SetupMaster{}.toCell());
    }

    receive(msg: BuyLevel){
        self.requireUserMain(msg.userId);
        let msgValue: Int = context().value;
        let balance: Int = myBalance() - msgValue;

        nativeThrowUnless(131,  msg.levelNumber > 0 &&  msg.levelNumber <= 12);

        let increment: Int = msg.levelNumber * self.gasMultiplier;
        let levelFee: Int = self.levelFees.get(msg.levelNumber)!!;
        let levelPrice: Int = self.levelPrices.get(msg.levelNumber)!!;

        let requireMinValue: Int = levelPrice + increment + levelFee;
        nativeThrowUnless(131, (requireMinValue <= msgValue || msg.userId == 1));
        
        nativeReserve(balance + levelFee, 0);
        self.totalProfit += levelPrice;
        let init: StateInit = initOf FtBaseProgramUser(msg.userId, myAddress());

        send(SendParameters{
            to: contractAddress(init),
            value: 0,
            mode: SendRemainingBalance,
            body: ActivateLevel{
                owner: msg.owner,
                invitedId: msg.invitedId,
                levelNumber: msg.levelNumber,
                levelPrice: levelPrice,
                recipientExcesses: msg.recipientExcesses
            }.toCell(),
            code: msg.levelNumber == 1 ? init.code : null,
            data: msg.levelNumber == 1 ? init.data : null
        });
    }

    receive(msg: UpdateLevelPrice){
        self.requireOwner();
        nativeThrowUnless(5, (msg.levelNumber > 0 && msg.levelNumber <= 12));
        self.levelPrices.set(msg.levelNumber, msg.levelPrice);
        self.reply("Level price successfully changed".asComment());
    }

    receive(msg: UpdateLevelFee){
        self.requireOwner();
        nativeThrowUnless(5, (msg.levelNumber > 0 && msg.levelNumber <= 12));
        self.levelFees.set(msg.levelNumber, msg.levelFee);
        self.reply("Level fee successfully changed".asComment());
    }

    receive(msg: UpdateGasMultiplier){
        self.requireOwner();
        nativeThrowUnless(5, msg.newValue > ton("0.5"));
        self.gasMultiplier = msg.newValue;
        self.reply("Gas multiplier successfully changed".asComment());
    }

    receive(msg: UpdateRecipientAddress){
        self.requireOwner();
        self.recipient = msg.newAddress;
        self.reply("Recipient address successfully changed".asComment());
    }

    // ------------------ Private Function  ------------------ //

    fun requireUserMain(id: Int){
        nativeThrowUnless(132, sender() == self.userMainAddress(id));
    }

    fun setupLevelPrice(){
        self.levelPrices.set(1, ton("1.0"));
        self.levelPrices.set(2, ton("2.0"));
        self.levelPrices.set(3, ton("4.0"));
        self.levelPrices.set(4, ton("7.0"));
        self.levelPrices.set(5, ton("12.0"));
        self.levelPrices.set(6, ton("22.0"));
        self.levelPrices.set(7, ton("40.0"));
        self.levelPrices.set(8, ton("70.0"));
        self.levelPrices.set(9, ton("120.0"));
        self.levelPrices.set(10, ton("220.0"));
        self.levelPrices.set(11, ton("400.0"));
        self.levelPrices.set(12, ton("790.0"));
    }

    fun setupLevelFee(){
        self.levelFees.set(1, ton("0.25"));
        self.levelFees.set(2, ton("0.5"));
        self.levelFees.set(3, ton("1.0"));
        self.levelFees.set(4, ton("1.75"));
        self.levelFees.set(5, ton("3.0"));
        self.levelFees.set(6, ton("5.5"));
        self.levelFees.set(7, ton("10.0"));
        self.levelFees.set(8, ton("17.5"));
        self.levelFees.set(9, ton("30.0"));
        self.levelFees.set(10, ton("55.0"));
        self.levelFees.set(11, ton("100.0"));
        self.levelFees.set(12, ton("197.5"));
    }

    // ------------------ Get Functions ------------------ //

    get fun programName(): String {
        return self.programName;
    }

    get fun gasMultiplier(): Int {
        return self.gasMultiplier;
    }

    get fun levelPrices(): map<Int as uint8, Int> {
        return self.levelPrices;
    }

    get fun levelFees(): map<Int as uint8, Int> {
        return self.levelFees;
    }

    get fun totalProfit(): Int {
        return self.totalProfit;
    }

    get fun masterAddress(): Address {
        return self.master;
    }

    get fun recipientAddress(): Address {
        return self.recipient;
    }

    get fun balance(): Int {
        return myBalance();
    }

    get fun userMainAddress(id: Int): Address{
        let init: StateInit = initOf FtUserMain(id, self.master);
        return contractAddress(init);
    }

    get fun programUserAddress(id: Int): Address{
        let init: StateInit = initOf FtBaseProgramUser(id, myAddress());
        return contractAddress(init);
    }
}
